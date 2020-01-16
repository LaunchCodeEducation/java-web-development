.. _tech-jobs-persistent:

Assignment #4: Tech Jobs (Persistent Edition)
=============================================

Your Task
---------

You will once again work with the ``techjobs`` application. This time around you'll add ORM
functionality by using Spring Data. You will be responsible for completing the code to allow users 
to create new job data.

Checkout and Review the Starter Code
------------------------------------

Fork and clone the starter code from the techjobs persistent repo.
TODO: link to the repo
TODO: describe what has changed from the end result of the last assignment. 

We're no longer using a csv file to load job data, instead, we'll be creating new Job objects via a 
user form. The Job data will be stored in a MySQL database that you'll setup in :ref:`Part 1 <tech-jobs-persistent-pt1>` of this assignment.

You'll next be tasked with completing the work to persist some of the classes of the job data. As you explore
the starter code, you'll notice that the ``JobField`` abstract class is no longer present. Your task for 
:ref:`Part 2 <tech-jobs-persistent-pt2>` is to complete the work to persist some of the classes.
TODO: clarify which classes they will need to complete.

The ``Job`` class will also look different from how you have last seen it. In Parts 3 and 4, you'll 
add back the ``employer`` and ``skills`` (formerly ``coreCompetency``) fields on the ``Job`` class,
using :ref:`one-to-many <tech-jobs-persistent-pt3>` and :ref:`many-to-many <tech-jobs-persistent-pt4>` relationships.

Finally, :ref:`Part 5 <tech-jobs-persistent-pt5>` asks you to be in charge of writing some SQL queries to extract the job 
data out of the application.

.. _tech-jobs-persistent-pt1:

Part 1: Setup the Database
--------------------------

Connect a database to a Spring App.

#. Start MySQL Workbench and create a new schema named ``techjobs``.

   .. admonition:: Tip
   
      Remember to double click on the schema name in the file tree to make it the default schema.

#. In the administration tab, create a new user, ``techjobs`` with the same settings as described in
   the lesson tutorial.
   TODO: reference the point in the book setting up the new user.

#. Update ``build.gradle`` with the dependencies.

#. Update ``src/resources/application.properties`` with the right info.

.. admonition:: Tip
   
   You can double check your setup against what you've already done for 
   :ref:`your coding events repo <setup-orm-database>`

.. _tech-jobs-persistent-pt2:

Part 2: Persisting Employers and Skills
---------------------------------------

You will need to have completed the :ref:`setup steps <tech-jobs-persistent-setup>` before starting this
section.

``AbstractEntity``
^^^^^^^^^^^^^^^^^^

We've replaced the abstract class ``JobField`` with an even more abstracted class aptly named, 
``AbstractEntity``. This class is holds the fields and methods that are common across the ``Job`` class
and the classes it contains as fields.  

#. We will be creating tables for the subclasses that inherit from
   ``AbstractEntity`` but not a table for this parent class. Therefore, give ``AbstractEntity`` the 
   ``@MappedSuperClass`` annotation.

#. Since all of the subclasses of ``AbstractEntity`` will be entities themselves, add the ``@Id`` 
   and ``@GeneratedValue`` annotations to the field ``id``.

#. Each subclass will also inherit the ``name`` field from ``AbstractEntity``. Add appropriate 
   validation annotations so that:
   
   a. a user cannot leave this field blank when creating an object. 

   b. there are reasonable limitations on the size of the name string.


Models
^^^^^^

In the last assignment, a ``Job`` object contained string fields for employer and core competency data. This employer 
and skill (formerly core competency) information about a particular job will now be stored in classes themselves.
These items themselves will hold their own supplementary information. 

#. Open the ``Employer`` model class. In addition to the fields inherited from ``AbstractEntity``, ``Employer`` should have a 
   string field for ``location``. Add this field with validation as you see fit, as well as getters and setters.

   .. admonition:: Note

      For the purposes of this application, an employer can only have one location.

#. ``Employer`` is a class that will be mapped to one of our tables. Make sure the class has the 
   ``@Entity`` annotation, as well as the no-arg constructor required for Hibernate to create an
   object.

#. In the model class ``Skill``, add a field for a longer description of the skill. Some hiring managers like to have
   more information available about the nature of a given programming language or framework. 

#. As with ``Employer``, give this class the ``@Entity`` annotation and be sure it contains a no-arg
   constructor.


Data Layer
^^^^^^^^^^

To map the ``Employer`` and ``Skill`` classes to your techjobs database, you'll add data access interfaces for these relational 
objects, similiar to the existing ``JobRepository`` interface. Like ``JobRepository``, make use of the Spring Data 
``CrudRepository`` class to map our objects.

#. In ``models/data``, create a new interface ``EmployerRepository``.

   a. ``EmployerRepository`` should extend ``CrudRepository``.
   #. ``EmployerRepository`` should be annotated with both ``@Repository`` and ``@Transactional``.

#. Repeat the steps above for an interface, ``SkillRepository``.

Controllers
^^^^^^^^^^^

With the employer repository in place, we will reference this to send object information through 
the ``EmployerController`` handlers. ``EmployerController`` contains two handlers with missing 
information.

#. View an individual employer object.

Your task here is to make use of the ``EmployerRepository`` class in these handlers. 

#. Add a private field of ``EmployerRepository`` type called ``employerRepository`` to 
   ``EmployerController``. Give this field an ``@Autowired`` annotation.

#. ``processAddEmployerForm`` already takes care of sending the form back if any of the submitted 
   employer object information is invalid. However, it doesn't yet contain the code to save a
   valid object. Use ``employerRepository`` and the appropriate method to do so.
   
#. ``displayViewEmployer`` will be in charge of rendering an a page to view the contents of an individual 
   employer object. It will make use of that employer object's ``id`` field to grab the correct
   information from ``employerRepository``. ``optEmployer`` currently initialized to ``null``. Replace this using
   the ``.findById()`` method with the right argument to look for the given employer object from 
   the data layer. 

   .. admonition:: Tip

      The variable holding the id you want to query for is already provided for you in the controller
      method's parameters.

#. Create a ``SkillController`` class and replicate the steps you followed above for ``EmployerController``.

Test It!
^^^^^^^^
The employer and skill view templates for adding and viewing these objects are made for you. Before you move on,
test your application now to make sure it runs as expected. You should be able to create Employer and Skill objects
and view them.

#. Start up your application – don’t forget to have our SQL server running – and go to the *Add Jobs*
   view from the application's navigation menu.

#. You won't be able to add a job yet, but you'll see a link to *Add Employers* and *Add Skills* in the form. Click them and proceed
   to check the functionality of the forms that follow.

#. Be sure to test your validation requirements and error handling.

When everything works, move on to Part 2 below.

.. admonition:: Tip

   If everything seems to work – that is, you are
   able to submit the form without any errors – but you don’t see your
   employers or skills in the list after submission, here’s what you should check:

   #. Is there any data in the ``employers`` and ``skills`` table? Check by going to MySQL Workbench
      and looking for the employer/skill data within your schema.

   #. If there’s data in the database, check that you are correctly
      querying for the list of all objects in the controller
      findAll()``?

   #. Ensure you’re passing the list into the view, and it is named the same as the variable in the ThymeLeaf template.


.. _tech-jobs-persistent-pt3:

Part 3: Setting Up a One-to-Many Relationship
---------------------------------------------

In this application, any one ``Job`` object is affiliated with one employer while one ``Employer`` may contain several jobs.

Now that you have set up persistence for the ``Employer`` and ``Skill`` classes, it is time to update the ``Job`` class
to make use of these. ``Job`` is already using the Spring Data framework to be persistent and now you'll update its 
``Employer`` field to create a one-to-many relationship. You'll also add a field on ``Employer`` to list the jobs associated 
with each instance.

Add a ``jobs`` Field to ``Employer``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Within ``Employer``, add a private property ``jobs`` of type
   ``List<Job>`` and initialize it to an empty ``ArrayList``. After we
   set up the ``Job`` class to work with ``Employer`` objects, this list
   will represent the list of all items in a given job. We’ll do this
   in a bit.

#. Use the ``@OneToMany`` and ``@JoinColumn`` annotations on the jobs list in ``Employer`` to declare the relationship between   
   data tables.

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

Update ``Job`` Model
^^^^^^^^^^^^^^^^^^^^

#. Since it too has ``id`` and ``name`` fields, the ``Job`` model class can also inherit from ``AbstractEntity``. Update the 
   class definition of ``Job`` to extend ``AbstractEntity``. Remove the redundant fields from ``Job``.

.. Using the ``Employer`` class as a field on Job objects will be much
.. more flexible, as it will allow users to create new employers
.. themselves.

#. Replace the type of the field ``employer`` to be of type ``Employer``. You will also need to refactor the affected constructor
   and getter and setter that use this field.

#. Add the ``@ManyToOne`` annotation on the field ``employer``

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

Updating ``HomeController``
^^^^^^^^^^^^^^^^^^^^^^^^^^^

We’ll make several updates here. Similar to what you have done in Part 1, several of the methods in ``HomeController`` are 
missing code because the class has not yet been *wired* with the data layer yet. 


#. Add a field ``employerRepository`` annotated with ``@Autowired``.
#. A user will select an employer when they create a job. Add the employer data from ``employerRepository`` into the form template.
   The add job form already includes an employer selection option. Be sure your variable name for the employer data matches that 
   already used in ``templates/add``. 
#. Checkout ``templates/add.html``. Make a mental note of the name of the variable being used to pass the selected employer 
   id on form submission.
#. In ``processAddJobForm``, add a parameter to the method to pass in the template variable you just found. You'll need to use the 
   ``@RequestParam`` annotation on this parameter. 
#. Still in ``processAddJobForm``, add code inside of this method to select the employer object that has been chosen to be 
   affiliated with the new job. You will need to select the employer useing the request parameter you've added to the method. 

   .. admonition:: Note

      An employer only needs to be found and set on the new job object if the form data is validated.



.. ``displayAddJobForm``
.. ~~~~~~~~~~~~~~~~~~~~~

.. #. A user will select an employer when they create a job. Add the employer data from ``employerRepository`` into the form template.
..    The add job form already includes an employer selection option. Be sure your variable name for the employer data matches that 
..    already used in ``templates/add``. 

.. .. We now need to pass in a list of categories into the view, rather the
.. .. array of enum values. Modify the appropriate line so that the ``model``
.. .. has an attribute ``"categories"`` equal to the result of calling
.. .. ``categoryDao.findAll()``.

.. .. Let’s take a detour to the ``cheese/add.html`` template to make sure
.. .. these categories are properly displayed in the form. Open that file, and
.. .. modify the section that renders the ``<select>`` element to look like
.. .. this:

.. .. .. code:: html

.. ..    <label th:for="type">Type</label>
.. ..    <select name="categoryId">
.. ..        <option th:each="category : ${categories}"
.. ..                th:text="${category.name}"
.. ..                th:value="${category.id}"></option>
.. ..    </select>

.. .. This loops over the list of categories, using the ``name`` and ``id``
.. .. properties to set up each value. Note also that we’ve set
.. .. ``name="categoryId"``, indicating that the posted property will be
.. .. called ``categoryId``.

.. processAddCJobForm
.. ~~~~~~~~~~~~~~~~~~

.. #. add request param from employer info on job object submission.
.. #. use .findbyId(). else.... to  select employer obj chosen
.. #. Job object .setEmployer

.. .. This action creates a new cheese. Based on our updates to ``add.html``
.. .. above, we can add ``categoryId`` to the method signature:

.. .. .. code:: java

.. ..    public String processAddCheeseForm(
.. ..                    @ModelAttribute  @Valid Cheese newCheese,
.. ..                    Errors errors,
.. ..                    @RequestParam int categoryId,
.. ..                    Model model)

.. .. We’ll need to have the ``Category`` object corresponding to this ID, so
.. .. we can set up the new cheese properly. Get it from the data layer like
.. .. this:

.. .. .. code:: java

.. ..    Category cat = categoryDao.findOne(categoryId);

.. .. This will fetch a single ``Category`` object, with ID matching the
.. .. ``CategoryID`` value selected. Then set it:

.. .. .. code:: java

.. ..    newCheese.setCategory(cat);

.. Review Job Deletion Code
.. ^^^^^^^^^^^^^^^^^^^^^^^^

.. #. have the students write soemthing to delete jobs?

.. .. The code to remove a ``Cheese`` object is already in place for you, but
.. .. since we won’t have a reason to use the ``delete`` method on a
.. .. ``CrudRepository`` interface, read the code in
.. .. ``displayRemoveCheeseForm`` and ``processRemoveCheeseForm`` to see how
.. .. to remove an item from the database.

.. Update Job View
.. ^^^^^^^^^^^^^^^

.. #. update view template to display employer info on given job object.

.. .. We’ve touched almost every file except the ``cheese/index.html``
.. .. template. Go into that file and update the table to display the category
.. .. name of a given cheese instead of its type. Update the header as well,
.. .. so it has “Category” in place of “Type”.

Test!
^^^^^

You made a lot of changes! Great work.

Assuming you don’t have any compiler errors, start up your
application. Don’t forget to start your SQL server. Make sure you can
create a new job object from the *Add Jobs* form, selecting a pre-existing employer. 

Then make sure the data has been saved in your job table. You should see a column for 
``employer_id``, corresponding to the employer object selected for the new job.

The *List* and *Search* functionality still isn't quite fixed so to view a job in the application, make a note 
of the job's id in the SQL table. Back in your browser, enter the path for ``/view/{jobId}``.


When everything works, move on to Part 3 below.

.. _tech-jobs-persistent-pt4:

Part 4: Setting Up a Many-to-Many Relationship
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

.. _tech-jobs-persistent-pt5:

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

.. Objectives
.. ----------

.. #. Setup the database
.. #. Configure an individual class to be managed by Spring Data
.. #. Configure a one-to-many relationship to be managed by Spring Data
.. #. Configure a many-to-many relationship to be managed by Spring Data
.. #. Create a SQL report