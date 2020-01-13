.. _tech-jobs-persistent:

Assignment #4: Tech Jobs (Persistent Edition)
=============================================

Your Task
---------

You will once again work with the ``techjobs`` application. This time around you'll add ORM
functionality by using Spring Data. 


Learning Objectives
-------------------

#. Configure an individual class to be managed by Spring Data
#. Configure a one-to-many relationship to be managed by Spring Data
#. Configure a many-to-many relationship to be managed by Spring Data
#. Create a SQL report

.. _tech-jobs-persistent-setup:

Setup
-----

Connect a database to a Spring App.


Part 1: Persisting a Single Class
---------------------------------

Be sure you’ve completed the :ref:`setup steps <tech-jobs-persistent-setup>` before starting this
section.

If you get stuck on any of the steps here, refer to the video lesson, or
other code within the program that was provided. You’ll often find the
answers there.

Setting Up the New Model
^^^^^^^^^^^^^^^^^^^^^^^^

We’ll use Spring Data – along with JPA and Hibernate – to create an
object-relational mapping for a new class.

#. update the classes: Job + Employer

#. use the @Entity annotation

#. id creation, getters and setters, constructors

#. id annotation, generated value annotation

#. validation annotations on fields

.. In ``org.launchcode.models``, create a new model class named
.. ``Category``. Add the ``@Entity`` annotation to make the class
.. persistent In other words, this annotation will ensure that the class is
.. mapped to a relational database table.

.. Give it a private ``id`` field that’s an ``int``, along with a private
.. ``name`` property that’s a string. Add a public getter and setter for
.. ``name``, but only a getter for ``id``. Other classes shouldn’t be able
.. to change our ID!

.. Mimic the same JPA annotations used in ``Cheese``:

.. .. code:: java

..    @Id
..    @GeneratedValue
..    private int id;

..    @NotNull
..    @Size(min=3, max=15)
..    private String name;

.. Add two constructors to ``Category``. - Default (no-argument)
.. constructor: This is required, and doesn’t need a any code within its
.. body. It will only be used by Hibernate in the process of creating
.. objects from data retrieved from the database. - A constructor that
.. accepts a parameter to set ``name``.

Setting Up the Data Layer
^^^^^^^^^^^^^^^^^^^^^^^^^

#. JobRepository interface creation, extend crud repo, transactional annotation

.. We’ll want instances of this class to be stored in the database, so
.. create a new interface in ``org.launchcode.models.data`` named
.. ``CategoryDao``. You can do this by creating a new class, and then
.. changing ``class`` to ``interface`` in the boilerplate code. It should
.. extend ``CrudRepository`` and have ``@Repository`` and
.. ``@Transactional`` annotations, as shown here:

.. .. code:: java

..    @Repository
..    @Transactional
..    public interface CategoryDao extends CrudRepository<Category, Integer> {
..    }

Adding Jobs
^^^^^^^^^^^

#. add JobRepository to homecontroller with @autowired annotation



.. Create a ``CategoryController`` in ``org.launchcode.controllers``. Add
.. the ``@Controller`` and ``@RequestMapping("category")`` annotations to
.. the class. Just inside the class, add:

.. .. code:: java

..    @Autowired
..    private CategoryDao categoryDao;

.. This creates a private field ``categoryDao`` of type ``CategoryDao``.
.. This object will be the mechanism with which we interact with objects
.. stored in the database. Recall that Spring will do the work of creating
.. a class that implements ``CategoryDao`` and putting one of those objects
.. in the ``categoryDao`` field when the application starts up. And all of
.. this is thanks to the ``@Autowired`` annotation.

.. This code would need to be added to each controller class that you want
.. to have access to the persistent collections defined within
.. ``categoryDao``.

.. .. raw:: html

..    <aside class="aside-warning">

.. We made the ``@Autowired`` annotation sound pretty dang magical! It’s
.. not that it isn’t, but don’t go adding ``@Autowired`` to every field
.. under the sun that you want to use and expect them to be initialized for
.. you.

.. Recall that ``@Autowired`` is part of Spring’s dependency injection
.. framework, and it works its magic in this case because we’re using
.. Spring’s ``CrudRepository`` interface, along with the ``@Repository``
.. annotations, and some other implicit Spring Boot settings.

.. .. raw:: html

..    </aside>

View All Jobs
^^^^^^^^^^^^^

#. create view template for accessing individual job info.

.. Create an ``index`` handler within ``CategoryController``. Create an
.. ``index.html`` template file in ``resources/templates/category/`` (you
.. will have to create this last folder).

.. The ``index`` handler should correspond to the route ``""`` (that is,
.. the path ``/category``), and it should retrieve the list of all
.. categories. This is done via the ``categoryDao`` object:
.. ``categoryDao.findAll()`` returns a collection (actually, an
.. ``Iterable``) of all ``Category`` objects managed by ``categoryDao``.
.. Use this snippet to retrieve the list of categories, and then pass the
.. list into the view by adding it to ``model``. Also add a ``"title"`` to
.. the model (“Categories” works).

.. The handler should render the ``index.html`` template that you just
.. created. This view should display an unordered list (that is, a
.. ``<ul>``) of category names. The list will look a bit plain for now, but
.. we will make it more interesting later on.

Add Jobs
^^^^^^^^

#. Next, we want to enable the user to create a new category via a form.
This will require multiple steps.

Add Handler Methods
^^^^^^^^^^^^^^^^^^^

Let’s add controller handlers to render and process the form.

#. create an add handler in homecontroller for adding jobs
#. create another handler for the posting of this form
#. check for object validation and if good, use the crudrepository mehtod to save the object

.. Create an ``add`` handler within ``CategoryController`` with input
.. parameter ``Model model``. It should create a new ``Category`` object
.. using the default constructor and pass it into the view with key
.. ``"category"`` (you can do this with the shorthand
.. ``model.addAttribute(new Category())``; note the omission of a
.. string/key argument). Add the title “Add Category” to ``model`` as well.

.. The ``add`` handler should accept ``GET`` requests at ``/category/add``
.. (recall that you set the path segment “category” at the controller level
.. already). The handler should render the ``category/add`` template (we’ll
.. add this template in a moment).

.. Create another ``add`` handler that accepts ``POST`` requests at
.. ``/category/add``. Its signature should be:

.. .. code:: java

..    public String add(Model model,
..        @ModelAttribute @Valid Category category, Errors errors)

.. Within this second ``add`` handler: - Determine whether or not there are
.. any validation errors. If there are, return the form at
.. ``category/add``. - If the form submission is valid: - Save the new
.. ``Category`` object by calling ``categoryDao.save(category)``. -
.. Redirect to the ``index`` handler for ``CategoryController`` by
.. returning the string ``"redirect:"``.

Add View
^^^^^^^^

#. create the template to add jobs via a form

.. In ``resources/templates/category/`` create a new template,
.. ``add.html``. Within the template, create a form that uses the
.. ``category`` object that you passed in from the controller.

.. You’ll need to bind the object to the form using
.. ``th:object="${category}"``. And you should use the appropriate
.. attributes within the form: ``th:for``, ``th:field``, ``th:errors``.

.. This is the same technique we’ve been using over the last couple of
.. weeks.

Adding Navigation Links
^^^^^^^^^^^^^^^^^^^^^^^

#. add a link to the add jobs form - TechJobs title in the nav bar

.. Let’s make it easy to navigate to the new views that we’ve created.

.. Within the ``fragments.html`` template, add a link to ``/category`` to
.. the list of navigation links.

.. Within the ``category/index.html`` template, add a link to
.. ``/category/add`` with the text “Add Category”. Place this link below
.. the list.

Test!
^^^^^

Start up your application – don’t forget to have our SQL server running – and try
to add a new job!

Click on the *TechJobs* navigation link, then on *Add Job*.
Complete the form, and if everything works as expected, you’ll see your
new job in the list. If everything seems to work – that is, you are
able to submit the form without any errors – but you don’t see your
job in the list, here’s what you should check:

-  Is there any data in the ``jobs`` table? Check by going to MySQL Workbench
   and looking for the job data within your schema.

.. hitting the *Open Start Page* button, then navigating to *Tools >
.. phpMyAdmin*. Find the ``cheese-mvc-data`` database, and look within
.. the ``categories``. If there isn’t any data in the table, you
.. probably forgot to save the category when processing the form.

-  If there’s data in the database, check that you are correctly
   querying for the list of all jobs in the controller
   findAll()``?
-  Ensure you’re passing this list into the view, and looping over the
   list of jobs to display them in the page.

When everything works, move on to Part 2 below.

Part 2: Setting Up a One-to-Many Relationship
---------------------------------------------

One job has one employer. One employer can have many jobs.


Add an Employer to a Job
^^^^^^^^^^^^^^^^^^^^^^^^

Within ``Employer``, add a private property ``jobs`` of type
``List<Job>`` and initialize it to an empty ``ArrayList``. After we
set up the ``Job`` class to work with ``Employer`` objects, this list
will represent the list of all items in a given job. We’ll do this
in a bit.

#. use the onetomany and join column annotations on the jobs list in Employer class

.. Add the following annotations:

.. .. code:: java

..    @OneToMany
..    @JoinColumn(name = "category_id")
..    private List<Cheese> cheeses = new ArrayList<>();

.. We’re setting up a one-to-many relationship: Each one category will have
.. many cheeses, but each cheese can have only one category. Hence, we use
.. the ``@OneToMany`` JPA annotation to declare this relationship.

.. We also add the ``@JoinColumn`` annotation with the parameter
.. ``name = "category_id"``. This tells Hibernate to use the
.. ``category_id`` column of the ``cheese`` table to determine which cheese
.. belong to a given category.

.. Hibernate will be very smart about this, storing and retrieving cheeses
.. and categories in a way that maintains their relationships to each
.. other. It will also populate this particular list for us, based on these
.. relationships.

Replace String Employer with Employer Object
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Using the ``Employer`` class as a field on Job objects will be much
more flexible, as it will allow users to create new employers
themselves.

#. add the @manytoone annotation on an employer field in Job

.. Within ``Cheese``, replace the ``type`` field with a field named
.. ``category``, of type ``Category``. Give it the ``@ManyToOne``
.. annotation, specifying that there can be many cheeses for any one
.. category.

.. .. code:: java

..    @ManyToOne
..    private Category category;

.. By setting up the field this way, Hibernate will create a column named
.. ``category_id`` (based on the field name) and when a ``Cheese`` object
.. is stored, this column will contain the ``id`` of its ``category``
.. object. The data for the ``category`` object itself will go in the table
.. for the ``Category`` class.

.. This complimentary pair of annotations – ``@ManyToOne`` and
.. ``@OneToMany``, along with ``@JoinColumn`` clarifying how the latter
.. should behave – set up this relationship to be managed properly on both
.. the application / object-oriented side and the database / relational
.. side.

.. Delete the ``CheeseType`` class by right-clicking on ``CheeseType.java``
.. in the package pane and selecting *Delete*. This will create
.. compiler/build errors where this type is used, but we’re about to fix
.. them!

Updating HomeController
^^^^^^^^^^^^^^^^^^^^^^^

We’ll make several updates here.

displayAddCheeseForm
~~~~~~~~~~~~~~~~~~~~

#. wire up homecontroller with the employerrepository.
#. update the addjob handlers so that they grab the employer information 
#. update the add job form to include an employer selection option

.. We now need to pass in a list of categories into the view, rather the
.. array of enum values. Modify the appropriate line so that the ``model``
.. has an attribute ``"categories"`` equal to the result of calling
.. ``categoryDao.findAll()``.

.. Let’s take a detour to the ``cheese/add.html`` template to make sure
.. these categories are properly displayed in the form. Open that file, and
.. modify the section that renders the ``<select>`` element to look like
.. this:

.. .. code:: html

..    <label th:for="type">Type</label>
..    <select name="categoryId">
..        <option th:each="category : ${categories}"
..                th:text="${category.name}"
..                th:value="${category.id}"></option>
..    </select>

.. This loops over the list of categories, using the ``name`` and ``id``
.. properties to set up each value. Note also that we’ve set
.. ``name="categoryId"``, indicating that the posted property will be
.. called ``categoryId``.

processAddCheeseForm
~~~~~~~~~~~~~~~~~~~~

This action creates a new cheese. Based on our updates to ``add.html``
above, we can add ``categoryId`` to the method signature:

.. code:: java

   public String processAddCheeseForm(
                   @ModelAttribute  @Valid Cheese newCheese,
                   Errors errors,
                   @RequestParam int categoryId,
                   Model model)

We’ll need to have the ``Category`` object corresponding to this ID, so
we can set up the new cheese properly. Get it from the data layer like
this:

.. code:: java

   Category cat = categoryDao.findOne(categoryId);

This will fetch a single ``Category`` object, with ID matching the
``CategoryID`` value selected. Then set it:

.. code:: java

   newCheese.setCategory(cat);

Review Cheese Deletion Code
---------------------------

The code to remove a ``Cheese`` object is already in place for you, but
since we won’t have a reason to use the ``delete`` method on a
``CrudRepository`` interface, read the code in
``displayRemoveCheeseForm`` and ``processRemoveCheeseForm`` to see how
to remove an item from the database.

One more thing…
---------------

We’ve touched almost every file except the ``cheese/index.html``
template. Go into that file and update the table to display the category
name of a given cheese instead of its type. Update the header as well,
so it has “Category” in place of “Type”.

Test!
-----

You made a lot of changes! Great work.

Assuming you don’t have any remaining compiler errors, start up your
application. (Don’t forget to start MAMP first!) Make sure you can
create a new cheese object, selecting a pre-existing category. Then make
sure the proper category name is displayed in the table on the home page
after doing so.

When everything works, move on to `Part 3 <../many-to-many/>`__.

Bonus Missions
--------------

-  Within ``CheeseController``, create a handler named ``category`` that
   responds to ``GET`` requests at URLs like ``/cheese/category/2``,
   where 2 may be the ID of any category in the system. This handler
   should retrieve all cheeses in the given category and pass them into
   the view. You should use the ``cheese/index.html`` template to
   display the results, with an appropriate title.

Many-To-Many
------------

Job to Skills

SQL Report
----------


How to Submit
-------------

To turn in your assignment and get credit, follow the :ref:`submission instructions <how-to-submit-work>`.

