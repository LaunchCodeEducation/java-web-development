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

displayAddJobForm
~~~~~~~~~~~~~~~~~

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

processAddCJobForm
~~~~~~~~~~~~~~~~~~

#. add request param from employer info on job object submission.
#. use .findbyId(). else.... to  select employer obj chosen
#. Job object .setEmployer

.. This action creates a new cheese. Based on our updates to ``add.html``
.. above, we can add ``categoryId`` to the method signature:

.. .. code:: java

..    public String processAddCheeseForm(
..                    @ModelAttribute  @Valid Cheese newCheese,
..                    Errors errors,
..                    @RequestParam int categoryId,
..                    Model model)

.. We’ll need to have the ``Category`` object corresponding to this ID, so
.. we can set up the new cheese properly. Get it from the data layer like
.. this:

.. .. code:: java

..    Category cat = categoryDao.findOne(categoryId);

.. This will fetch a single ``Category`` object, with ID matching the
.. ``CategoryID`` value selected. Then set it:

.. .. code:: java

..    newCheese.setCategory(cat);

Review Job Deletion Code
^^^^^^^^^^^^^^^^^^^^^^^^

#. have the students write soemthing to delete jobs?

.. The code to remove a ``Cheese`` object is already in place for you, but
.. since we won’t have a reason to use the ``delete`` method on a
.. ``CrudRepository`` interface, read the code in
.. ``displayRemoveCheeseForm`` and ``processRemoveCheeseForm`` to see how
.. to remove an item from the database.

Update Job View
^^^^^^^^^^^^^^^

#. update view template to display employer info on given job object.

.. We’ve touched almost every file except the ``cheese/index.html``
.. template. Go into that file and update the table to display the category
.. name of a given cheese instead of its type. Update the header as well,
.. so it has “Category” in place of “Type”.

Test!
^^^^^

You made a lot of changes! Great work.

Assuming you don’t have any remaining compiler errors, start up your
application. (Don’t forget to start your SQL server first.) Make sure you can
create a new job object, selecting a pre-existing employer. Then make
sure the proper employer name is displayed in the table on the home page
after doing so.

When everything works, move on to Part 3 below.


Part 3: Setting Up a Many-to-Many Relationship
----------------------------------------------

A Job requires many skills and a skill can be associated with several jobs.

Creating the Skill Model
^^^^^^^^^^^^^^^^^^^^^^^^

This final section of the studio has us set up a many-to-many
relationship between two classes. The classes in question will be
``Job`` and ``Skill``. 

.. We don’t have the latter in place yet, so let’s
.. get it set up.

The Skill Class
~~~~~~~~~~~~~~~

#. add @entity annotaiton to skill class
#. add a field named Jobs that is a list
#. add the @manytomany annotation to this field

.. Create a new class named ``Menu`` in ``org.launchcode.models``. It
.. should have the ``@Entity`` annotation at the class level.

.. It should also have a ``name`` field that’s a string, an ``id`` field
.. that’s an integer, and a field named ``cheeses`` of type
.. ``List<Cheese>``. This latter field will be used to hold all items in
.. the menu, and Hibernate will populate it for us based on the
.. relationships we set up in our controllers. Be sure to add getter and
.. setter methods for these fields, though note that ``cheeses`` should not
.. have a setter (why?).

.. Add JPA annotations to each of these fields. The ``id`` and ``name``
.. fields should get the same annotations as the corresponding fields in
.. the ``Cheese`` class. Be sure you understand what each of these does as
.. you are adding it.

.. Apply the ``@ManyToMany`` annotation to the ``cheeses`` list. This will
.. set up one half of our many-to-many relationship.

.. We want to be able to add items to our menu, so implement a method with
.. the following signature:

.. .. code:: java

..    public void addItem(Cheese item)

.. This method should simply add the given item to the list.

.. Finally, add two constructors: an empty default constructor, and one
.. that accepts a value for, and sets, ``name``.

The SkillRepository Interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. create Skills Repository witht he right super class and annotations

.. Now that the ``Skill`` class is set up to be persistent, we need to
.. enable Spring Data to store and retrieve instances of the class.

.. Create a ``SkillRepository`` interface in ``org.launchcode.models.data``,
.. following the pattern of previously-created interfaces in this package.
.. This will allow us to access ``Menu`` objects via the data layer from
.. within our controllers. Be sure to add the necessary annotations, as you
.. did with ``CategoryDao``.

Setting Up the Other Side of the Relationship
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. add the manytomany annotation onto a skills field in the job class
#. add the mapped by skills argument

.. Back in the ``Job`` class, add this field:

.. .. code:: java

..    @ManyToMany(mappedBy = "cheeses")
..    private List<Menu> menus;

.. This field will configure the other side of our many-to-many
.. relationship. It represents the list of ``Menu`` objects that a given
.. cheese is contained in. In order to tell Hibernate how to store and
.. populate objects from the list, we specify that the field should be
.. ``mappedBy`` the ``cheeses`` field of the ``Menu`` class.

.. In other words, the items in this list should correspond to the ``Menu``
.. objects that contain a given ``Cheese`` object in their ``cheeses``
.. list. And the inverse relationship is true as well: The items in
.. ``Menu.cheeses`` should correspond to the ``Cheese`` objects that have a
.. given ``Menu`` object in their ``menus`` list. Hibernate will notice
.. that our list contains ``Menu`` objects, and will look in that class for
.. a property with the same name as that specified by the ``mappedBy``
.. attribute.

.. We won’t be accessing ``menus`` outside this class, so there’s no need
.. currently to make it anything other than ``private``.

.. .. raw:: html

..    <aside class="aside-note">

.. There are multiple ways that we could have set up this relationship
.. using JPA annotations. When looking at documentation, you’ll surely see
.. variations of this configuration.

.. .. raw:: html

..    </aside>

The SkillController Class and Views
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. add skillrepository as autowired field to home controller so that a new job can be added with skills

.. There are lots of changes to the controller and view layers that we’ll
.. need to make to fully enable usage of our new model class across the
.. application.

.. Within ``org.launchcode.controllers`` create a new class,
.. ``MenuController``. At the top of the class, use ``@Autowired`` to
.. declare instances of ``MenuDao`` and ``CheeseDao`` that should be
.. initialized by Spring Boot.

.. Be sure to configure your controller with ``@Controller`` and
.. ``@RequestMapping(value = "menu")``.

.. List Skills
.. ^^^^^^^^^^^

.. We will now set up the view that displays a list of all menus in the
.. system.

.. Write a handler method ``index`` that uses ``menuDao`` to retrieve all
.. menus and display them in a list within the template
.. ``resources/templates/menu/index.html`` (the rest of our templates will
.. be in this same folder, so we’ll omit the full path for the rest of this
.. part of the studio). You’ll have to create the ``menu/`` folder within
.. ``templates/``.

.. Each menu in the list should link to a URL of the form ``/menu/view/5``,
.. where 5 could be the ID of any menu. Add these links now, and we’ll set
.. up the handler to process these requests in a moment.

.. Within the ``index.html`` template, add a link below the list to the URL
.. ``/menu/add``. We’ll set up this page next.

.. .. raw:: html

..    <aside class="aside-note">

.. Each template that you create in this part of the studio should use the
.. ``head`` and ``navigation`` fragments from
.. ``resources/templates/fragments.html``.

.. .. raw:: html

..    </aside>

.. Add a Skill
.. -----------

.. Display the Add Skill Form
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~

.. We want to allow users to add new, empty menus via a form. This is our
.. next task.

.. In ``MenuController``, create a handler method named ``add`` that
.. responds to ``GET`` requests, and which displays the ``add.html``
.. template. The handler should also pass in a new ``Menu`` object created
.. by calling that class’ default constructor. We’ll use this object to
.. help render the form.

.. Within ``add.html``, create a form that has the ``menu`` object bound to
.. it using ``th:object``. Add a single form input to accept the name of
.. the new menu, along with a ``<span>`` element that can display any
.. validation errors. Be sure to use ``th:for``, ``th:field``, and
.. ``th:errors`` in creating the label, input, and span elements.

.. The form should ``POST`` to the same URL at which it is displayed.

.. Process the Add Menu
.. ~~~~~~~~~~~~~~~~~~~~

.. Once the form is posted, we’ll need process the data on the server.

.. In ``MenuController`` create a handler method named ``add`` that
.. responds to ``POST`` requests. It should accept a valid ``Menu`` object
.. passed in via model binding, along with the corresponding ``Errors``
.. object.

.. Check for the existence of errors. If errors exist, render the
.. ``add.html`` form again. If not, save the ``Menu`` object using
.. ``menuDao.save()`` (passing in your valid ``Menu`` instance). Then,
.. redirect to ``return "redirect:view/" + menu.getId()``. We’ll se up this
.. handler and view template next.

.. View a Menu
.. -----------

.. Let’s create functionality to allow the user to view the contents of a
.. menu. As a reminder, we linked each menu to a URL. (Please remember to
.. check your navigation links.)

.. In ``MenuController``, create a handler named ``viewMenu`` that accepts
.. ``GET`` requests at URLs like ``view/5``, where 5 can be any menu ID.
.. You’ll need to use the correct syntax within the ``@RequestMapping``
.. annotation, along with the ``@PathVariable`` annotation on a method
.. parameter that you’ll add (which should be an ``int``).

.. Within the handler, retrieve the ``Menu`` object with the given ID using
.. ``menuDao``. Pass the given menu into the view.

.. .. raw:: html

..    <aside class="aside-note">

.. In the video lesson demonstrating this part of the application, the
.. name, ID, and list of cheeses are each passed in separately to the view.
.. Passing in the full ``Menu`` object, as we do here, is more efficient.

.. .. raw:: html

..    </aside>

.. The ``viewMenu`` method should render the ``view.html`` template. Let’s
.. build that template now.

.. Create ``view.html`` in the folder that contains your other templates
.. associated with this controller. It should display the name of the menu
.. as the page title. It should display a list of menu items in a ``<ul>``
.. element. Note that you’ll need to loop over ``menu.cheeses`` (here we
.. assume you’ve passed in the menu with the attribute name ``menu``; if
.. not, modify accordingly).

.. Below the list, add the following link:

.. .. code:: html

..    <p><a th:href="'/menu/add-item/' + ${menu.id}">Add Cheese</a></p>

.. This will link to a form that we are about to create.

.. Add Menu Items
.. --------------

.. We can create menus, and view them, but as of now, any menu we create
.. would be empty! Let’s address that.

.. Within ``MenuController``, create a method named ``addItem`` that
.. responds to ``GET`` request of like ``add-item/5``, where 5 can be any
.. menu ID. As above, you’ll need to use the correct syntax within the
.. ``@RequestMapping`` annotation, along with the ``@PathVariable``
.. annotation on a method parameter that you’ll add (which should be in
.. ``int``).

.. Retrieve the menu with the given ID using ``menuDao``.

.. AddMenuItemForm
.. ~~~~~~~~~~~~~~~

.. To aid in validation and display of this form, let’s create a model
.. class to represent the form. Create a new package, ``forms``, within
.. ``org.launchcode.models``. Within that package, create the
.. ``AddMenuItemForm`` class. This class will not be persistent, so there’s
.. no need to add ``@Entity``.

.. We’ll need two fields to render the form: ``private Menu menu`` and
.. ``private Iterable<Cheese> cheeses``. Add accessors for each of these.

.. We’ll need two fields to process the form: ``private int menuId`` and
.. ``private int cheeseId``. These will need accessors as well. Further, we
.. want to be able to validate that these fields are not ``null``, so add
.. the appropriate annotation to do so.

.. Finally, add two constructors: a default no-arg constructor and one that
.. accepts and sets values for ``menu`` and ``cheeses``. The default
.. constructor is needed for model binding to work.

.. Rendering the Form
.. ~~~~~~~~~~~~~~~~~~

.. Now, back in ``MenuController.addItem``, create an instance of
.. ``AddMenuItemForm`` with the given ``Menu`` object, as well as the list
.. of all ``Cheese`` items in the database. Pass this form object into the
.. view with the name ``"form"``, along with a title that reads “Add item
.. to menu: MENU NAME” (using the actual menu name).

.. This handler should render the form ``add-item.html``. Make sure it
.. returns the correct string to do so, and then create this template.

.. The template should contain a form that posts to ``/menu/add-item``, and
.. renders the form using the ``form`` attribute that was passed in. Use
.. ``th:object`` to bind ``form`` to the ``<form>`` element, and display a
.. ``<select>`` element that contains all of the cheeses. The ``name`` of
.. this input should be ``cheeseId``, and the ``value`` attribute of each
.. ``<option>`` should be the ``id`` of the given cheese. This will result
.. in the ID of the item to add being passed in the request. Be sure to use
.. ``th:for``, ``th:field``, and ``th:errors`` in creating the label,
.. input, and span elements.

.. Below the ``<select>``, add this input:

.. .. code:: html

..    <input type="hidden" name="menuId" th:value="*{menu.id}" />

.. This will pass the ID of the menu in the post request, but will not be
.. visible to the user.

.. Add a submit button, and you’re ready to process the form!

.. Process the Form
.. ~~~~~~~~~~~~~~~~

.. Back in ``MenuController``, create another handler named ``addItem``
.. that responds to ``POST`` requests at ``/menu/add-item``. It should
.. accept a valid ``AddMenuItemForm`` object via model binding, along with
.. the associated ``Errors`` object.

.. Check for errors, rendering the ``"menu/add-item"`` template again if
.. there are any.

.. If there are no errors, find the given ``Cheese`` and ``Menu`` by ID,
.. using the respective DAO objects, and add the item to the menu. Use
.. ``menuDao`` to save the menu: ``menuDao.save(theMenu)``.

.. .. raw:: html

..    <aside class="aside-warning">

.. If the menu isn’t saved here, the changes will not be pushed to the
.. database, and hence will be lost.

.. .. raw:: html

..    </aside>

.. To finish this handler, redirect to the URL corresponding to the full
.. menu view for this menu. This was created above, and we leave it to you
.. to figure out the correct redirect URL.

Clean Up the Navigation
-----------------------

#. to the navbar, add options to view a list of employers and skills

.. Let’s improve the navigation of our app. In
.. ``resources/templates/fragments.html`` modify the header navigation
.. fragment so that it displays a menu like this:

.. The *Menus* link should link to ``/menu``.

.. And in ``resources/templates/cheese/index.html``, ensure the navigation
.. links below the table look like this:

Test!
-----

Run your application and make sure you can create a new job with several skills.

When everything works, you’re done! Congrats!


SQL Report
----------


How to Submit
-------------

To turn in your assignment and get credit, follow the :ref:`submission instructions <how-to-submit-work>`.


.. Part 2 Bonus Mission
.. --------------------

.. -  Within ``CheeseController``, create a handler named ``category`` that
..    responds to ``GET`` requests at URLs like ``/cheese/category/2``,
..    where 2 may be the ID of any category in the system. This handler
..    should retrieve all cheeses in the given category and pass them into
..    the view. You should use the ``cheese/index.html`` template to
..    display the results, with an appropriate title.

.. Part 3 Bonus Missions
.. ---------------------

.. -  Add the ability to edit a ``Cheese``. To do this, follow the
..    instructions outlined in `Class 8 Prep
..    Exercises <../../../class-prep/8/exercises.html>`__, with the
..    following modifications. In steps 5 and 9, rather than using
..    ``CheeseData`` to get and save the object, use ``cheeseDao``. And
..    don’t forget to call ``.save()`` to make sure your edits are stored
..    in the database!.