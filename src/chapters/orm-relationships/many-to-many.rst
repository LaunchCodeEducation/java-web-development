Creating a Many-to-Many Relationship
====================================

Just as when introducing one-to-one relationships, our first step in exploring many-to-many relationships is to introduce a new class to relate to ``Event``.

Persistent Tags - Video
-----------------------

.. youtube::
   :video_id: bLK-VtZgx0Q
   :gh_path: LaunchCodeEducation/coding-events/add-tags

Persistent Tags - Text
----------------------

To create a persistent ``Tag`` class, we follow the same steps as when making ``Event`` and ``EventCategory`` classes persistent, with no relationships. To review these steps, refer to :ref:`orm1-exercises`.

Creating a Many-to-Many Relationship - Video
--------------------------------------------

.. youtube::
   :video_id: qtbkUXAjpt4
   :gh_path: LaunchCodeEducation/coding-events/many-to-many

Creating a Many-to-Many Relationship - Text
-------------------------------------------

As you might guess, a many-to-many relationship can be configured with the JPA annotation ``@ManyToMany``. We can set up both sides of the ``Event``/``Tag`` relationship with this annotation.

In ``Event``:

.. sourcecode:: java
   :lineno-start: 30

   @ManyToMany
   private final List<Tag> tags = new ArrayList<>();

This ensures that Hibernate creates a relationship from a given event to every ``Tag`` instance placed in its ``tags`` collection.

In ``Tag``:

.. sourcecode:: java
   :lineno-start: 20

   @ManyToMany(mappedBy = "tags")
   private final List<Event> events = new ArrayList<>();

Along with the ``@ManyToMany`` annotation, the ``mappedBy`` paramater ensures that Hibernate populates the ``events`` collection of a given ``Tag`` object with every ``Event`` object that has that specific tag in *its* ``tags`` collection.

These minor additions fully configure the many-to-many relationship. Making use of this relationship in our controllers and views will take quite a bit more work, however. 

Many-to-Many Forms and Data Transfer Objects - Video
----------------------------------------------------

.. youtube::
   :video_id: 1qMaEv_CJ6k
   :gh_path: LaunchCodeEducation/coding-events/many-to-many-features

Many-to-Many Forms and Data Transfer Objects - Text
---------------------------------------------------

.. index:: design pattern

In order to make use of our new many-to-many relationship, we need to have a way for users to add a tag to an event. We will implement this feature by creating a form that, for a given event, lets the user add a single tag. The process of binding an ``Event`` and a ``Tag`` object together will be made easier through the use of a new design pattern. 

.. _dto:

Data Transfer Objects (DTO)
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. index:: ! data transfer object

A **data transfer object** (or DTO) is an object that enables multiple other objects or values to be passed around an application, in a single container. For reasons that will make more sense shortly, we will want to utilize a DTO to hold ``Event`` and ``Tag`` instances that we want to relate to each other.

A DTO for these two classes is very simple. It contains two fields, a no-arg constructor, and accessors for the fields. Each field is annotated with ``@NotNull`` because we will use this class in conjunction with model binding and form processing. 

.. sourcecode:: java
   :lineno-start: 11

   public class EventTagDTO {

      @NotNull
      private Event event;

      @NotNull
      private Tag tag;

      public EventTagDTO() {}

      public Event getEvent() {
         return event;
      }

      public void setEvent(Event event) {
         this.event = event;
      }

      public Tag getTag() {
         return tag;
      }

      public void setTag(Tag tag) {
         this.tag = tag;
      }
   }

We place this class in a new package, ``dto``, contained within the ``models`` package. It is a model since it structures data that our application uses. However, it is not persistent (there is no ``@Entity`` annotation) because we won't need to store it in the database. 

Connecting Two Objects 
^^^^^^^^^^^^^^^^^^^^^^

The process of connecting two many-to-many objects is similar to that of connecting objects with other types of relationships. We need a form that can allow a user to create a new relationship, and processing the form should result in the relationship being saved to the database.

Rendering the Form
++++++++++++++++++

Given a specific event, we want to be able to render a form that allows the user to add a tag to that event. This means that the form has to know *which event* the user wants to work with. One way to do this is with query parameters. 

For example, say a user wants to add a tag to the ``Event`` object with ID 13. To get to the form that enables this, they may navigate to ``/events/add-tag?eventId=13``. This request will return a form that allows a tag to be added to *only* the event with ID 13.

Here is the handler method in ``EventController`` that renders the form, broken down line-by-line just below.

.. sourcecode:: java
   :lineno-start: 112

   @GetMapping("add-tag")
   public String displayAddTagForm(@RequestParam Integer eventId, Model model){
      Optional<Event> result = eventRepository.findById(eventId);
      Event event = result.get();
      model.addAttribute("title", "Add Tag to: " + event.getName());
      model.addAttribute("tags", tagRepository.findAll());
      EventTagDTO eventTag = new EventTagDTO();
      eventTag.setEvent(event);
      model.addAttribute("eventTag", eventTag);
      return "events/add-tag.html";
   }

- **Line 112**: Specifies that the handler will be available at the route ``/events/add-tag``, and will respond to ``GET`` requests.
- **Line 113**: Defines the ``displayAddTagForm`` handler, which has a required query parameter, ``eventId``.
- **Line 114**: Queries the repository for the ``Event`` object with ID equal to the value of ``eventId``.
- **Line 115**: Extracts the ``Event`` object from the result of the query. We would ideally include a conditional to check that such an object exists before proceeding, but are omitting it here to focus on DTO usage.
- **Line 116**: Creates a title for the form, which includes the name of the event.
- **LIne 117**: Passes a collection of all available tags into the view. This collection will be used to render a dropdown that the user can use to select the tag to be added.
- **Line 118**: Creates an empty ``EventTagDTO`` object. This will be used to help render the form, as we have done previously with model classes.
- **Line 119**: Assigns the ``event`` property of the ``eventTag`` DTO object. This will enable us to reference the specific event when rendering the form, so we can assign the tag to the correct event.
- **Line 120**: Passes the DTO into the view.
- **Line 121**: Returns the name of the template containing the form.

While this may seem like a lot of new concepts, it really isn't. If you look closely, the one new thing that we are doing is using a DTO class to bind an *existing* event to the form. The other steps here are variations of thing you have done before.

Now let's look at the form in ``events/add-tag.html``.

.. sourcecode:: html
   :linenos:

   <!DOCTYPE html>
   <html lang="en" xmlns:th="http://www.thymeleaf.org/">
   <head th:replace="fragments :: head"></head>
   <body class="container">

   <header th:replace="fragments :: header"></header>

   <form method="post">
      <div class="form-group">
         <input type="hidden" th:field="${eventTag.event}">
         <select th:field="${eventTag.tag}">
               <option th:each="tag : ${tags}"
                     th:value="${tag.id}"
                     th:text="${tag.name}"
               ></option>
         </select>
      </div>
      <input type="submit" class="btn btn-success" value="Add Tag">
   </form>

   </body>
   </html>

This form has two inputs. The first---with ``th:field="${eventTag.event}"``---is hidden, since it should not be modified by the user. We use it to keep track of the specific event that we are about to add a tag to.

The second field, the ``select`` element, is bound to the ``eventTag.tag`` field. The dropdown contains each of the available tags in our application. 

When this form is submitted, it will have all of the information necessary to create an ``EventTagDTO`` object using model binding.

Processing the Form
+++++++++++++++++++

As with ``displayAddTagForm``, we will break down the form's ``POST`` handler in ``EventController`` in detail.

.. sourcecode:: java
   :lineno-start: 124

   @PostMapping("add-tag")
   public String processAddTagForm(@ModelAttribute @Valid EventTagDTO eventTag,
                                 Errors errors,
                                 Model model){

      if (!errors.hasErrors()) {
         Event event = eventTag.getEvent();
         Tag tag = eventTag.getTag();
         if (!event.getTags().contains(tag)){
               event.addTag(tag);
               eventRepository.save(event);
         }
         return "redirect:detail?eventId=" + event.getId();
      }

      return "redirect:add-tag";
   }

Using model binding, our method takes a valid parameter of type ``EventTagDTO``. Since we referenced the ``event`` and ``tag`` fields of our DTO when rendering the form (in the template, using ``th:field``), our submitted form should contain all of the data necessary to create an ``EventTagDTO`` instance. This instance will be valid if both ``event`` and ``tag`` are non-null. 

The reasons for creating a DTO model should hopefully be a bit clearer by now. Using a DTO allows us to create and validate these objects through model binding. The same event and tag relationship information could be processed without a DTO, but this would require passing query parameters for the IDs of both ``event`` and ``tag`` objects, querying the ``eventRepository`` and ``tagRepository`` for these items, validating those objects, etc. Simply put, the DTO makes this procedure cleaner and easier.

Once we have a valid DTO, lines 130-131 retrieve the values of its. Then, as long as the given event doesn't already have the given tag, we add the tag to it's collection in lines 132-134. Finally, we save the ``event`` to ``eventRepository``, which results in the relationship being stored in the database.

Exactly *how* this relationship is stored utilizes a new type of SQL table.

Join Tables
^^^^^^^^^^^

Think about how relationships are established at the database level. One-to-one and one-to-many relationships are facilitated by the use of a foreign key column on one side of the relationship. Our ``event`` table has two foreign key columns: ``event_category_id`` and ``event_details_id``. 

For a given row in ``event``, the column ``event_category_id`` contains the primary key of the row in ``event_category`` that the ``event`` row is related to, and similarly for ``event_details_id``. 

The only difference is the *number* of different ``event`` rows that may have the same value of ``event_category_id`` and ``event_details_id``. The ``event``/``event_category`` relationship is many-to-one, so *many* event rows may have the same ``event_category_id`` value. The ``event``/``event_details`` relationship is one-to-one, so *only one* event row may have a certain value in ``event_details_id``. 

.. index:: ! join table

Using foreign and primary keys to create many-to-many relationships is a bit trickier. In order to relate rows in ``event`` to rows in ``tag`` we need need a third table, known as a **join table**. A join table consists of two columns, each of which is a foreign key column to another table. Each row in a join table represents a relationship between one row in each of the two tables. This technique enables many-to-many relationships.

Consider some example data in our ``event`` and ``tag`` tables.

.. list-table:: Sample ``event`` data
   :header-rows: 1

   * - id
     - name
     - event_category_id
     - event_details_id
   * - 13
     - WWDC
     - 2
     - 14
   * - 15
     - SpringOne Platform
     - 2
     - 16
   * - 17
     - Java meetup
     - 3
     - 18
   
.. list-table:: Sample ``event_category`` data
   :header-rows: 1

   * - id
     - name
   * - 2
     - Conference
   * - 3
     - Meetup

.. list-table:: Sample ``tag`` data
   :header-rows: 1

   * - id
     - name
   * - 4
     - ios
   * - 5
     - spring
   * - 6
     - java

A join table for these two tables would be called ``event_tags``, and would have two columns, ``event_id`` and ``tag_id``. Each of these columns are foreign key columns into their respective tables. 

If we want to relate the ``ios`` tag to the ``WWDC`` event, we create a new row in ``event_tags``:

.. list-table:: A join table with a single relationship
   :header-rows: 1

   * - events_id
     - tags_id
   * - 13
     - 4

We can do this again and again to generate more relationships. Let's revisit the many-to-many diagram from earlier in the chapter. 

.. figure:: figures/many-to-many.png
   :alt: Three Event objects on the left, with various relationships to three Tag objects on the right
   :width: 800px

   A many-to-many relationship between Event and Tag objects

The join table representing these relationships looks like this:

.. list-table:: The full join table representing the relationships in the figure above
   :header-rows: 1

   * - events_id
     - tags_id
   * - 13
     - 4
   * - 15
     - 5
   * - 15
     - 6
   * - 17
     - 6

When configuring a many-to-many relationship with Hibernate and JPA annotations, a join table will be automatically created and populated for you. Pretty cool, huh? 

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: Model binding only works when using a persistent class.

.. ans: False. Any class may be used with model binding

.. admonition:: Question

   The use of join tables enables (select all that apply):

   #. A database where you never need to run a ``JOIN`` query.
   #. Many-to-many relationships between tables.
   #. Many-to-many relationships between classes without using the ``@ManyToMany`` annotation.
   #. Rainbows and butterflies to be stored in your database.

.. ans: B only.
