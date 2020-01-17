.. _tech-jobs-persistent:

Assignment #4: Tech Jobs (Persistent Edition)
=============================================

Your Task
---------

You will once again work with the ``Tech Jobs`` application. This time around you'll add ORM
functionality by using Spring Data. You will be responsible for completing the code to allow users 
to create new job data.

Your final application will have the same list and search capabilities as your :ref:`Tech Jobs (MVC Edition) <tech-jobs-mvc>` but 
you'll need to do the work to connect the project to a database for storing user-submitted job data.

Checkout and Review the Starter Code
------------------------------------

Fork and clone the starter code from the `techjobs persistent repository <https://github.com/LaunchCodeEducation/java-web-dev-techjobs-persistent>`__.

You won't be able to run your application yet. You'll need to complete :ref:`Part1 <tech-jobs-persistent-pt1>` before you can
check out the app in the browser. That said, it's a good idea to get familiar with the classes and templates even before you're able
to execute ``bootRun``.

We're no longer using a csv file to load job data, instead, we'll be creating new Job objects via a 
user form. The Job data will be stored in a MySQL database that you'll setup in :ref:`Part 1 <tech-jobs-persistent-pt1>` of this assignment.

You'll next be tasked with completing the work to persist some of the classes of the job data. As you explore
the starter code, you'll notice that the ``JobField`` abstract class is no longer present. Your task for 
:ref:`Part 2 <tech-jobs-persistent-pt2>` is to complete the work to persist some of the classes.
You'll do this for ``Employer`` and ``Skill`` classes, as well as ``Job``.

The ``Job`` class will also look different from how you have last seen it. In Parts 3 and 4, you'll 
add object relational mapping on the ``Job`` class by refactoring the ``employer`` and ``skills`` (formerly ``coreCompetency``) 
fields. 

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

Test It!
^^^^^^^^

When your database is properly configured, you should have no compiler errors when starting the application. Execute ``bootRun``
and check the compiler output to make sure this is the case. If all runs, you will be able to view your app running locally in 
the browser at ``Localhost:8080`` (unless of course you have changed the server port).

Your running application still has limited functionality. You won't yet be able to add a job from the *Add Job* form. You also
won't yet be able to view the list of jobs or search for jobs - but this is mostly because you have no more job data. Move on to
Part 2 below to get the app to be more useful.

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
   #. ``EmployerRepository`` should be annotated with ``@Repository``.

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

Update ``Job`` Model
^^^^^^^^^^^^^^^^^^^^

#. Since it too has ``id`` and ``name`` fields, the ``Job`` model class can also inherit from ``AbstractEntity``. Update the 
   class definition of ``Job`` to extend ``AbstractEntity``. Remove the redundant fields from ``Job``.

#. Replace the type of the field ``employer`` to be of type ``Employer``. You will also need to refactor the affected constructor
   and getter and setter that use this field.

#. Add the ``@ManyToOne`` annotation on the field ``employer``

.. _data-in-homecontroller:

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


Test It!
^^^^^^^^

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

Using a many-to-many relationship, we can now use the ``Skill`` object to store a ``Job`` object's skills. At the moment, 
a job can have many skills listed as strings. In this section, you'll be tasked with changing this field type to be a list
of skills. Just as a job requires many skills, any skill can be associated with several jobs. With this in mind, you'll also 
add a list of jobs as a field onto the skill class.


``Skill.jobs``
^^^^^^^^^^^^^^

#. In your ``Skill`` class, add a jobs field.

   #. What type should this field be?

   #. This field has a many-to-many type relationship with skills. You'll need to add the ``@ManyToMany`` annotation 
      with an argument ``mappedBy="skills"`` to ensure this mapping.

Refactor ``Job.skills``
^^^^^^^^^^^^^^^^^^^^^^^

#. Update your ``Job`` model class to fit its many-to-many relationship with skills.

   #. ``Job.skills`` already exists. What needs to change and/or be added to map this relationship.

      .. admonition:: Tip

         Be sure to check the whole class for any necessary type updates.


Updating ``HomeController``, Again
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You next need to wire ``HomeController`` now with the skills data in order to add skills objects to a new job.
This will look almost precisely like what you have done for employer data above. Refer back to 
:ref:`this section <data-in-homecontroller>` to inject the controller with skill data. 

There is, however, one difference to keep in mind. The job form being processed only accepts one employer by an ``id``
field. Many skills can be added to a single job, though. Here's what we'll say about how to send the right skills along with 
the job form.

#. The code for the view has already been written. Look in ``templates/add.html``. You'll see a form-group section that iterates
   over available skills data and renders a checkbox for each skill. Each checkbox input contains an attribute ``name="skills"``.
#. You'll need to pass in that attribute value to ``processAddJobForm`` in ``HomeController`` as a ``@RequestParam``. 

   .. sourcecode:: java

      @RequestParam List<Integer> skills

#. Then, to get the skills data from a list of ids (rather than a single id as we did with employer), use the ``CrudRepository`` method
   ``.findAllById(ids)``.

   .. sourcecode:: java

      List<Skill> skillObjs = (List<Skill>) skillRepository.findAllById(skills);
      newJob.setSkills(skillObjs);

   .. admonition:: Note
   
      As with a job's employer, you only need to query your database for skills if the job model is valid.


It's Your Job, List It and Re-Search It
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You now have all the tools in place to re-implement the list and search views from :ref:`tech-jobs-mvc>`.

#. In the ``ListController`` class, add fields for ``EmployerRepository`` and ``SkillRepository``, both annotated with 
   ``@Autowired``.
#. You'll also need to pass the employer and skill data from those repositories into the view template rendered at ``list/``.
   Add the right ``model.addAttribute(name, value)`` statements to pass this info into ``templates/list.html``.    

Test It!
^^^^^^^^

Run your application and make sure you can create a new job with an employer and several skills. You should now also have restored
full list and search capabilities.

When everything works, you’re done! Congrats!

.. _tech-jobs-persistent-pt5:

SQL Report
----------

TBD! 


How to Submit
-------------

To turn in your assignment and get credit, follow the :ref:`submission instructions <how-to-submit-work>`.

