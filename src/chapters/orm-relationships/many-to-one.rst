Creating a Many-to-One Relationship
===================================

The first relationship we implement will be between the ``Event`` and ``EventCategory`` classes. We will allow multiple events to be in the same category, but each event will only have one category. Thus, this will be a many-to-one relationship.

Before diving in, let's reduce repetition in our persistent classes, that is, let's DRY out our code.

Creating an ``AbstractEntity`` - Video
--------------------------------------

.. youtube::
   :video_id: GKOCCjn86yk
   :gh_path: LaunchCodeEducation/coding-events/abstract-entity

Creating an ``AbstractEntity`` - Text
-------------------------------------

The steps needed to implement ``AbstractEntity`` are outlined in :ref:`orm1-studio`.

Setting Up the Relationship - Video
-----------------------------------

We are now ready to create a relationship between ``Event`` and ``EventCategory``.

.. youtube::
   :video_id: aFr_E2T7zZ8
   :gh_path: LaunchCodeEducation/coding-events/many-to-one

Setting Up the Relationship - Text
----------------------------------

Our many-to-one relationship is established in the ``Event`` class; each event will have one category, and there may be many events in a given category. 

Currently, similar functionality is enabled via the ``EventType`` field of ``Event``. However, ``EventType`` is an enum, which means that new values can not be added without changing the code and re-compiling. Using the persistent ``EventCategory`` class to organize events will be a much more flexible and user-friendly approach. 

Replacing ``EventType`` With ``EventCategory``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the ``Event`` class, replace the ``type`` field with a new private field of type ``EventCategory``:

.. sourcecode:: java
   :lineno-start: 25

   private EventCategory eventCategory;

This will introduce compiler errors wherever ``type`` is referenced. We will fix these shortly.

First, however, update ``Event`` so that:

#. Its main constructor (i.e. NOT the no-arg constructor) takes a parameter of type ``EventCategory`` and uses it to initialize ``eventCategory``.
#. It has a getter/setter pair for ``eventCategory``.
#. The ``eventCategory`` field has the ``@NotNull`` validation annotation, along with an appropriate message.

This establishes a relationship between the two classes, but that relationship is not yet *persistent*. To configure Hibernate to keep track of this relationship in the database, we add the ``@ManyToOne`` annotation to ``eventCategory``. 

.. sourcecode:: java
   :lineno-start: 27

   @ManyToOne
   @NotNull(message = "Category is required")
   private EventCategory eventCategory;

This annotation informs Hibernate that there can be many events for each category, but only one category per event. 

Before we can start up the app and test our changes, we need to remove the code that references the deleted ``type`` field. A quick way to find these references is to find ``EventType`` in the *Project* pane of IntelliJ, right-click, and select *Find Usages*. This will open a pane listing each location where ``EventType`` occurs in our project, whether that is an object of that type or a direct reference to the class itself. 

.. figure:: figures/find-usages.png
   :alt: The search results pane after running Find Usages on EventType
   :width: 600px

   All remaining references to ``EventType`` in our project

The first occurrence is in ``EventController.displayCreateEventForm``:

.. sourcecode:: java
   :lineno-start: 35

   model.addAttribute("types", EventType.values());

This line passes a collection of all of the values of ``EventType`` into the view, to be rendered in the form used to create new events.

Since we are now using ``EventCategory`` to group events, our code should instead be passing in all of the category objects in our app. To fetch category objects, we need an instance of ``EventCategoryRepository`` in our controller. Add an ``@Autowired`` instance to the top of the controller:

.. sourcecode:: java
   :lineno-start: 24

   @Autowired
   private EventCategoryRepository eventCategoryRepository;

Now, use the repository to fetch all saved categories:

.. sourcecode:: java
   :lineno-start: 40

   model.addAttribute("categories", eventCategoryRepository.findAll());

This line replaces the line references ``EventType.values()``. Notice that we have relabeled this attribute ``"categories"`` 
to be more consistent. This also requires updating the ``events/create.html`` template:

.. sourcecode:: html
   :lineno-start: 27

   <div class="form-group">
      <label>Category
      <select th:field="${event.eventCategory}">
         <option th:each="eventCategory : ${categories}"
                  th:value="${eventCategory.id}"
                  th:text="${eventCategory.name}"
         ></option>
      </select>
      <p class="error" th:errors="${event.eventCategory}"></p>
      </label>
   </div>

This new template code includes several changes:

#. The ``select`` is now bound to the field ``eventCategory``.
#. The loop references ``categories`` and has an updated iterator variable name, ``eventCategory``.
#. The value of the ``select`` is now ``eventCategory.id``. This allows model binding to occur upon form submission. Spring Boot will determine the category object to assign to the new event object by referencing the ``id``.
#. The text for each ``option`` is now ``eventCategory.name``
#. The error message display now references the new field, ``event.eventCategory``.

The remaining usages of ``EventType`` refer to:

#. An ``Event`` constructor parameter.
#. The getter/setter pair for ``type`` in ``Event``.
#. An import statement in ``EventController``.
#. The ``EventType`` class itself.

Removing this unneeded code resolves all remaining compiler errors. 

The ``events/index.html`` template needs to be updated as well, since it still contains a reference to the ``type`` field of ``Event``:

.. sourcecode:: html
   :lineno-start: 23

   <td th:text="${event.type}"></td>

This usage wasn't found by IntelliJ because templates do not receive compile-time type checking like classes do. The updated version looks like this:

.. sourcecode:: html
   :lineno-start: 23

   <td th:text="${event.eventCategory.name}"></td>

Testing and Database Updates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Before starting up the application, let's look at our ``event`` table:

.. figure:: figures/event-table-before-update.png
   :alt: The event table before starting up the application
   :width: 600px

   The ``event`` table will be updated the next time the app starts

Notice that the ``type`` column remains, even though we have deleted the ``type`` field from the ``Event`` class. The next time we start up the application, Hibernate will attempt to update the schema to match the structure of our updated model class. 

.. index:: ! truncate

.. admonition:: Tip

   Notice that existing events will not have a category, which violates our new ``@NotNull`` validation rule. The easiest way to handle this is to delete all rows in ``event``.
   
   To delete all events, truncate the ``event`` table in MySQL Workbench. (To **truncate** a SQL table is simply to delete all its rows.) To do this, select the table in the *Schemas* pane, right-click, and select *Truncate Table...*

Start up the application and refresh the view in MySQL Workbench. 

.. figure:: figures/event-table-after-update.png
   :alt: The event table after starting up the application
   :width: 600px

   The ``event`` retains the ``type`` column, but has a new ``event_category_id`` column

Notice that there is a new column, ``event_category_id``. This new column has type ``int`` and is a foreign key column to the ``event_category`` table. References to objects in Java are translated into foreign-key references by Hibernate. 

.. admonition:: Note

   You may find it odd that the ``type`` column is *still* present, even after restarting. Hibernate will not drop columns from a table even if that field is removed from the corresponding class. 

   Hibernate will generally avoid deleting your data, since you may want to keep it around (even if just in the form of a backup). You can simply drop this column yourself.

.. admonition:: Tip

   If your table was not updating upon restarting, make sure you have ``spring.jpa.hibernate.ddl-auto`` set to ``update`` in ``application.properties``.

If we create some new events, we can see precisely how ``event`` rows are related to ``event_category`` rows.

.. figure:: figures/event-table-with-data.png
   :alt: The event table with two rows

   The ``event`` table with new data

.. figure:: figures/event-category-table-with-data.png
   :alt: The event_category table with two rows


   The ``event_category`` table 

Notice that our events have ``event_category_id`` values of ``12`` and ``13`` (these values may differ slightly in your application). These are foreign keys into the ``event_category`` table. For example, in the tables above, the ``event`` row with ``id`` equal to ``14`` is related to the ``event_category`` row with ``id`` equal to ``12``. This database relationship corresponds to the relationship between objects that was created by Spring Boot when we submitted the form.

With this many-to-one relationship in place, we next look at how to establish a persistent one-to-many relationship.

Check Your Understanding
------------------------

.. admonition:: Question

   What is the annotation that allows ``@AbstractEntity`` to handle logic related to IDs/primary keys of subclasses, 
   yet not be mapped to a database table.

.. ans: short answer, @MappedSuperclass


.. admonition:: Question

   You are working on a Spring application tracking elected officials. Your model class, ``Senator`` has a many-to-one relationship 
   with another model class, ``State``. To properly configure this relationship in the Hibernate context, what must be present?

   #. In ``Senator``, a ``state`` field, annotated with ``@OneToMany``
   #. In ``Senator``, a ``state`` field, annotated with ``@ManyToOne``
   #. In ``State``, a ``senator`` field, annotated with ``@OneToMany``
   #. In ``State``, a ``senator`` field, annotated with ``@ManyToOne``

.. ans: b. In ``Senator``, a ``state`` field, annotated with ``@ManyToOne``
