Creating a One-to-One Relationship
==================================

We :ref:`defined a one-to-one relationship <one-to-one-def>` between two objects, A and B, as occurring when an object of type A can be related to only one instance of an object of type B, and vice versa.

Such a relationship can be configured using the JPA annotation ``@OneToOne``.

Creating a One-to-One Relationship - Video
------------------------------------------

.. youtube::
   :video_id: 0yNIbAcd4ng
   :gh_path: LaunchCodeEducation/coding-events/one-to-one

Creating a One-to-One Relationship - Text
-----------------------------------------

We first need a class that makes sense to relate to ``Event`` in a one-to-one fashion.

The ``EventDetails`` Class
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. index:: design pattern

Given a class that contains lots of metadata, it is a common design pattern is to create a class to encapsulate all such data. For example, many apps will have a ``UserProfile`` class to model the data associated with a ``User`` class, such as a profile photo, interests, connections, and so on. 

We will follow this pattern to create an ``EventDetails`` class to model the data associated with an ``Event``. This will provide a great opportunity to set up a one-to-one relationship. And while we don't have a lot of data associated with events yet, this will set up our application to grow as we add more.

To start, create a new class in the ``models`` packaged named ``EventDetails``. Like all of our model classes, it should be annotated with ``@Entity`` and extend ``AbstractEntity``. Then move the ``description`` and ``contactEmail`` fields out of ``Event`` and into ``EventDetails``. Finally, add constructors and accessor methods.

``EventDetails`` now looks like this:

.. sourcecode:: java
   :lineno-start: 11

   @Entity
   public class EventDetails extends AbstractEntity {

      @Size(max = 500, message = "Description too long!")
      private String description;

      @NotBlank(message = "Email is required")
      @Email(message = "Invalid email. Try again.")
      private String contactEmail;

      public EventDetails(String description, String contactEmail) {
         this.description = description;
         this.contactEmail = contactEmail;
      }

      public EventDetails() {}

      public String getDescription() {
         return description;
      }

      public void setDescription(String description) {
         this.description = description;
      }

      public String getContactEmail() {
         return contactEmail;
      }

      public void setContactEmail(String contactEmail) {
         this.contactEmail = contactEmail;
      }
   }

Back in the ``Event`` class, clean up by removing all references to ``description`` and ``contactEmail``. 

Relating ``EventDetails`` to ``Event``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each ``Event`` should have a single ``EventDetails`` object, and vice versa. Breaking out metadata into a separate class allows us to grow ``EventDetails``---for example, adding location, date, time, and attendance information---without making ``Event`` too big. It also allows our application to load a set of ``Event`` objects without also needing to fetch lots of additional metadata if it isn't needed. 

To establish the relationship, add a new field of type ``EventDetails`` to ``Event`` and annotate it with ``@OneToOne``. Additionally, add the validation annotations ``@Valid`` and ``@NotNull``. 

.. sourcecode:: java
   :lineno-start: 22

   @OneToOne
   @Valid
   @NotNull
   private EventDetails eventDetails;

.. index:: @Valid

This is the first time we have used ``@Valid`` on a class member. 

First, let's review what ``@NotNull`` accomplishes. When an Event object is created, the ``@NotNull``annotation will ensure that the ``eventDetails`` field is not null. But what if we also want to ensure that ``eventDetails`` is itself a valid object? 

By default, model validation will not descend into the ``eventDetails`` class to check *its* validation annotations. However, annotating the field with ``@Valid`` overrides the default behavior. It makes sure that an ``Event`` object will not be considered valid unless it has an ``EventDetails`` object that is *also* valid (i.e. it has valid ``description`` and ``contactEmail`` fields).

As we have seen, using ``@Valid`` on a method parameter in a controller will result in the fields of that method being validated. For instance, with an ``Event`` object, our ``@NotNull`` annotation will ensure that the ``eventDetails`` field is not null. By default, however, validation will not descend into the ``eventDetails`` class to check *its* validation annotations. 

Using ``@Valid`` on the ``eventDetails`` field ensures that such validation occurs. It makes sure that an ``Event`` object will not be considered valid unless it has an ``EventDetails`` object that is *also* valid (i.e. it has valid ``description`` and ``contactEmail`` fields).

Before moving on, create a getter and setter pair for ``eventDetails``.

Template Updates
^^^^^^^^^^^^^^^^

Our ``events/create.html`` and ``events/index.html`` templates reference the fields ``event.description`` and ``event.contactEmail``, which no longer exist. We need to update those references to use the new ``eventDetails`` field.

In ``events/index.html``:

.. sourcecode:: java
   :lineno-start: 18

   <tr th:each="event : ${events}">
      <td th:text="${event.id}"></td>
      <td th:text="${event.name}"></td>
      <td th:text="${event.eventDetails.description}"></td>
      <td th:text="${event.eventDetails.contactEmail}"></td>
      <td th:text="${event.eventCategory.name}"></td>
   </tr>

Notice that lines 21 and 22 now reference ``description`` and ``contactEmail`` off of ``event.eventDetails``.

Similarly, update ``events/create.html``:

.. sourcecode:: java
   :lineno-start: 15

   <div class="form-group">
      <label>Description
         <input th:field="${event.eventDetails.description}" class="form-control">
      </label>
      <p class="error" th:errors="${event.eventDetails.description}"></p>
   </div>
   <div class="form-group">
      <label>Contact Email
         <input th:field="${event.eventDetails.contactEmail}" class="form-control">
      </label>
      <p class="error" th:errors="${event.eventDetails.contactEmail}"></p>
   </div>

The inputs and error elements associated with ``description`` and ``contactEmail`` have now similarly been updated. With these changes in place, model binding in our controller will take place properly.

Cascading ORM Operations
^^^^^^^^^^^^^^^^^^^^^^^^

We have one final update to make. To illustrate, let's look at our ``POST`` handler for creating and saving ``Event`` objects:

.. sourcecode:: java
   :lineno-start: 65

   @PostMapping("create")
   public String processCreateEventForm(@ModelAttribute @Valid Event newEvent,
                                       Errors errors, Model model) {
      if(errors.hasErrors()) {
         model.addAttribute("title", "Create Event");
         return "events/create";
      }

      eventRepository.save(newEvent);
      return "redirect:";
   }

The ``newEvent`` parameter is created by Spring Boot using model binding. As usual, we validate the new model object using ``@Valid`` in conjunction with the ``errors`` object. 

.. admonition:: Note

   Recall that validation annotations within ``EventDetails`` will be checked (for the ``Event.eventDetails`` field) since we added ``@Valid`` to that field.

If you were to start your application and run it at this point, an exception would occur when attempting to save ``newEvent`` on line 73 (``eventRepository.save(newEvent)``). Specifically, the root exception would be:

::

   org.hibernate.TransientPropertyValueException: Not-null property references a transient value - 
   transient instance must be saved before current operation : 
   org.launchcode.codingevents.models.Event.eventDetails -> 
   org.launchcode.codingevents.models.EventDetails

.. index:: ! transient

This exception refers to the transient value ``Event.eventDetails``. A **transient** value is a an object that *can* be saved to the database (i.e. is of an entity type) but has NOT been saved yet. In our case, trying to save ``newEvent`` causes problems because its ``eventDetails`` field can not be null in the database, but the value of this field---a new ``EventDetails`` object created on form submission---has not been saved yet.

.. index:: ! cascade

The fix for this problem is simple, and allows us to introduce the concept of cascading. A database operation **cascades** from ``Event`` to ``EventDetails`` if, when the operation is applied to an ``Event`` instance, it is also applied to the associated ``EventDetails`` instance. If our call to ``eventRepository.save`` could be made to *cascade* then our problem would be solved! 

To cascade our save operation, go into the ``Event`` class and add a ``cascade`` parameter to the ``@OneToOne`` annotation:

.. sourcecode:: java
   :lineno-start: 22

   @OneToOne(cascade = CascadeType.ALL)
   @Valid
   @NotNull
   private EventDetails eventDetails;

The ``cascade`` parameter specifies which ORM operations should cascade from ``Event`` to its ``eventDetails`` field. Setting this to ``CascadeType.ALL`` specifies that *all* database operations---including save and delete---should cascade. 

We *could* set ``cascade = CascadeType.PERSIST`` and solve our current problem as well. However, that would mean that delete operations would not cascade. It makes sense for the ``EventDetails`` object to be deleted when its associated ``Event`` object is deleted, so we use ``CascadeType.ALL``.

As you continue working with ORM, you are likely to need to use other ``CascadeType`` values. We won't go into more depth on this topic here, but encourage you to `read the documentation <https://docs.oracle.com/javaee/6/api/javax/persistence/CascadeType.html>`_ on your own.

At this point, your app should work. We have established our first one-to-one relationship, while learning about a new design pattern and cascading. Nice work! 

The Inverse Relationship
^^^^^^^^^^^^^^^^^^^^^^^^

Once we have set up the relationship from ``Event`` to ``EventDetails``, it is easy to configure the inverse relationship. We don't need to do this for the functionality currently in ``coding-events``, but we will walk through the steps here for demonstration purposes. 

To do so, add a field of type ``Event`` to ``EventDetails``. Then add ``@OneToOne`` to the new field with a ``mappedBy`` parameter.

.. sourcecode:: java

   @OneToOne(mappedBy = "eventDetails")
   private Event event;

Setting ``mappedBy = "eventDetails"`` will ensure that the field is populated correctly. For a specific ``EventDetails`` object ``details``, ``event`` will be populated with the ``Event`` object that contains ``details``. Then both sides of the one-to-one relationship will have a reference to the other.

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: When a new object is saved to a repository, all of its non-primitive fields are saved as well.

.. ans: False. Any fields that are also entities must be either explicitly as well, or else the appropriate cascade setting must be used.

.. admonition:: Question

   Consider an entity type A that has a reference to an entity type B, both of which are stored in a SQL database. Which of the following are true?

   #. A and B are in a one-to-one relationship.
   #. A is not valid unless B is also valid.
   #. Setting ``cascade = CascadeType.ALL`` on the relationship annotation ensures that B is saved whenever A is saved.
   #. A and B will have a foreign-key relationship in the database.

.. ans: C and D. Answer A is not true since the relationship may be many-to-one. Answer B is not true since the @Valid annotation must be applied to fields for this to happen.
