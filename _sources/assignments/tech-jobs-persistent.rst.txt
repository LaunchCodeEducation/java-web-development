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

Each of the four sections of this assignment will also ask you to demonstrate your SQL skills under an item labelled **SQL TASK**.

As you work through each part, refer to our `demo app <https://techjobs-persistent.launchcodetechnicaltraining.org/>`_ to clarify questions about intended application behavior.


Checkout and Review the Starter Code
------------------------------------

Set up a local copy of the project:

#. In Canvas, **Graded Assignment #4: TechJobs (Persistent Edition)** contains a GitHub Classroom assignment invitation link and then set up the project in IntelliJ. Refer back to the GitHub Classroom instructions from :ref:`assignment0` for details. 
#. Launch the application (via the Gradle pane, *Tasks > Application >
   bootRun*) to make sure it starts up properly. Then shut it down.
#. The tests for this assignment are set up the same way as for :ref:`assignment 2 <assignment-2-autograding>`.

You won't be able to run your application or the tests yet. If you try to do so, you'll see a host of errors relating to the
Spring Data annotations and classes. Some of these have already been used in the code, but the dependency that includes them has not yet been declared. That will be one of your tasks. You'll need to complete :ref:`Part1 <tech-jobs-persistent-pt1>` before you can
run the application and view it in a browser.

That said, it's a good idea to scan the classes and templates even before you're able to execute
``bootRun``. Take a gander at the ``Job`` class. It will look somewhat similar to the model in
:ref:`Tech Jobs (MVC Edition) <tech-jobs-mvc>`, with a few key differences.

You're no longer using a csv file to load job data, instead, we'll be creating new Job objects via a
user form. The Job data will be stored in a MySQL database that you'll setup in :ref:`Part 1 <tech-jobs-persistent-pt1>` of this assignment.

As you explore
the starter code, you'll notice that the ``JobField`` abstract class is no longer present. Your task for
:ref:`Part 2 <tech-jobs-persistent-pt2>` is to complete the work to persist some of the classes.
You'll do this for ``Employer`` and ``Skill`` classes, as well as ``Job``.

The ``Job`` class will also look different from how you have last seen it. In Parts 3 and 4, you'll
add object relational mapping on the ``Job`` class by refactoring the ``employer`` and ``skills`` (formerly ``coreCompetency``)
fields.

In your IntelliJ project, you'll see an empty file in the root directory called ``queries.sql``. After completing the
Java updates for parts 1,2,3, and 4, we ask you to test your application updates with SQL statements.

Since you are entering your own data, the queries we ask you to write will return unique result sets. For example, if you haven't entered
any data yet, there may be an empty result set. However, as the architect of the database, you have the knowledge to write the
appropriate queries nonetheless.

.. _tech-jobs-persistent-pt1:

Part 1: Connect a Database to a Spring App
------------------------------------------

#. Start MySQL Workbench and create a new schema named ``techjobs``.

   .. admonition:: Tip

      Remember to double click on the schema name in the file tree to make it the default schema.

#. In the administration tab, create a new user, ``techjobs`` with the same settings as described in
   the lesson tutorial. This user should have the password ``techjobs`` as well.

#. Update ``build.gradle`` with the necessary dependencies. At this point, you should be able to run the tests. Run the tests in `TestTaskOne` to verify your gradle dependencies.

#. Update ``src/resources/application.properties`` with the correct info. This will include
   ``spring.datasource.url`` set to the address of your database connection, as well as the username and password
   for a user you have created. Refer to the tip below for the other properties you must add to complete your
   database setup.

.. admonition:: Tip

   You can double check your setup against what you've already done for
   :ref:`your coding events repo <setup-orm-database>`. You can copy these property assignments from your coding
   events repo, only needing to change the database address and username/password values.

.. admonition:: Tip

   If when starting your application, you encounter an error similar to

   .. sourcecode:: bash

      com.mysql.cj.exceptions.InvalidConnectionAttributeException: The server time zone value 'CDT' is unrecognized …

   then add `?useLegacyDatetimeCode=false&serverTimezone=America/Chicago` to the end of your `spring.datasource.url` value.

Test It with SQL
^^^^^^^^^^^^^^^^

When your database is properly configured, you should have no compiler errors when starting the application. Execute ``bootRun``
and check the compiler output to make sure this is the case. If everything runs, you will be able to view your app
locally in the browser at ``Localhost:8080`` (unless of course you have changed the server port).

#. In your MySQL workbench, open a new query tab to check your database connection.

#. **SQL TASK:** At this point, you will have one table, ``job``. In ``queries.sql`` under "Part 1", list the columns and their data types in the table as a SQL comment.

Your running application still has limited functionality. You won't yet be able to add a job with the *Add Job* form. You also
won't yet be able to view the list of jobs or search for jobs - but this is mostly because you have no job data. Move on to
Part 2 below to start adding these functionalities.


.. _tech-jobs-persistent-pt2:

Part 2: Persisting Employers and Skills
---------------------------------------

You will need to have completed the :ref:`setup steps <tech-jobs-persistent-pt1>` before starting this
section.

``AbstractEntity``
^^^^^^^^^^^^^^^^^^

We've replaced the abstract class ``JobField`` with an even more abstracted class aptly named,
``AbstractEntity``. This class holds the fields and methods that are common across the ``Job`` class
and the classes it contains as fields.

#. We will be creating tables for the subclasses that inherit from
   ``AbstractEntity`` but not a table for this parent class. Therefore, give ``AbstractEntity`` the
   ``@MappedSuperclass`` annotation.

#. Since all of the subclasses of ``AbstractEntity`` will be entities themselves, add the ``@Id``
   and ``@GeneratedValue`` annotations to the field ``id``.

#. Each subclass will also inherit the ``name`` field from ``AbstractEntity``. Add appropriate
   validation annotations so that:

   a. a user cannot leave this field blank when creating an object.

   b. there are reasonable limitations on the size of the name string. Keep in mind that the name field will be
      shared across ``Job``, ``Employer``, and ``Skill`` classes. Some employer names might be longer than 50 characters.


Models
^^^^^^

In the last assignment, a ``Job`` object contained string fields for employer and core competency data. This employer
and skill (formerly core competency) information about a particular job will now be stored in classes themselves.
These items themselves will hold their own supplementary information.

#. Open the ``Employer`` model class. In addition to the fields inherited from ``AbstractEntity``, ``Employer`` should have a
   string field for ``location``. Add the field for ``location`` with validation that ensures it is not empty and has a reasonable length. In addition, add public accessor methods
   to ``Employer``.

   .. admonition:: Note

      For the purposes of this application, an employer can only have one location.

#. ``Employer`` is a class that will be mapped to one of our tables. Make sure the class has the
   ``@Entity`` annotation, as well as the no-arg constructor required for Hibernate to create an
   object.

#. In the model class ``Skill``, add a field for a longer description of the skill, named ``description``, with public accessor methods. Some hiring managers like to have
   more information available about the nature of a given programming language or framework.

#. As with ``Employer``, give this class the ``@Entity`` annotation and be sure it contains a no-arg
   constructor.


Data Layer
^^^^^^^^^^

To map the ``Employer`` and ``Skill`` classes to your ``techjobs`` database, you'll add data access interfaces for these relational
objects, similar to the existing ``JobRepository`` interface. Like ``JobRepository``, make use of the Spring Data
``CrudRepository`` interface to map our objects.

#. In ``models/data``, create a new interface ``EmployerRepository``.

   a. ``EmployerRepository`` should extend ``CrudRepository``.
   #. ``EmployerRepository`` should be annotated with ``@Repository``.

#. Repeat the steps above for an interface, ``SkillRepository``.

Controllers
^^^^^^^^^^^

.. admonition:: Warning

   The tests in ``TestTaskTwo`` relating to the following tasks have been commented out because they depend on the code you wrote earlier. Open ``TestTaskTwo`` in IntelliJ and find these tests. For each one:

   #. Select the entire commented-out method. These methods start around line 328. You may need to add ``import`` statements for some of the classes used in these methods.
   #. Uncomment the method by using ``cmd+/`` on Mac or ``ctrl+/`` on Windows.

   If you do not uncomment these tests, your code will not pass the autograder. 
   
   Uncommenting these methods will introduce some new errors related to a class named ``SkillController``, but these will be fixed by the code you are about to write. If you like, you can leave these commented out until you get to that task.

With the employer repository in place, we will reference this to send object information through
the ``EmployerController`` handlers. ``EmployerController`` contains two handlers with missing
information. Your task here is to make use of the ``EmployerRepository`` class in these handlers.

#. Add a private field of ``EmployerRepository`` type called ``employerRepository`` to
   ``EmployerController``. Give this field an ``@Autowired`` annotation.

#. Add an ``index`` method that responds at ``/employers`` with a list of all employers in the database. This method should use the template ``employers/index``. To figure out the name of the model attribute you should use to pass employers into the view, review this template.

#. ``processAddEmployerForm`` already takes care of sending the form back if any of the submitted
   employer object information is invalid. However, it doesn't yet contain the code to save a
   valid object. Use ``employerRepository`` and the appropriate method to do so.

#. ``displayViewEmployer`` will be in charge of rendering a page to view the contents of an individual
   employer object. It will make use of that employer object's ``id`` field to grab the correct
   information from ``employerRepository``. ``optEmployer`` is currently initialized to ``null``. Replace this using
   the ``.findById()`` method with the right argument to look for the given employer object from
   the data layer.

   .. admonition:: Tip

      The variable holding the id you want to query for is already provided for you in the controller
      method's parameters.

#. Create a ``SkillController`` class and replicate the steps you followed above for ``EmployerController``. The new controller should have the methods, ``index``, ``displayAddSkillForm``, ``processAddSkillForm``, and ``displayViewSkill``. These methods should behave exactly as the corresponding methods in ``EmployerController``. The relevant templates have already been created for you.

   At this point, uncomment all remaining methods in ``TestTaskTwo``, if you have not done so already. You'll need to add an ``import`` statement for the new controller to the test file.

Test It with SQL
^^^^^^^^^^^^^^^^

The employer and skill view templates for adding and viewing these objects are made for you. Before you move on,
test your application now to make sure it runs as expected. You should be able to create Employer and Skill objects
and view them.

#. Start up your application – don’t forget to have your SQL server running – and go to the *Add Jobs*
   view from the application's navigation menu.

#. You won't be able to add a job yet, but you'll see a link to *Add Employers* and *Add Skills* in the form. Click them and proceed
   to check the functionality of the forms that follow.

#. Be sure to test your validation requirements and error handling.

#. **SQL TASK:** In ``queries.sql`` under "Part 2", write a query to list the names of the employers in St. Louis City. Do NOT specify an ordering for the query results. 

.. admonition:: Tip

   If everything seems to work – that is, you are
   able to submit the form without any errors – but you don’t see your
   employers or skills in the list after submission, here’s what you should check:

   #. Is there any data in the ``employers`` and ``skills`` table? Check by going to MySQL Workbench
      and looking for the employer/skill data within your schema.

   #. If there’s data in the database, check that you are correctly
      querying for the list of all objects in the controller
      Are you calling ``.findAll()`` on the repository?

   #. Ensure you’re passing the list into the view, and it is named the same as the variable in the ThymeLeaf template.

   When everything works, move on to Part 3 below.

Throughout your work, refer to the `demo app <https://techjobs-persistent.launchcodetechnicaltraining.org/>`_ as needed.

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
   data tables. Recall that this annotation needs a ``name`` parameter. What should its value be? 

Update ``Job`` Model
^^^^^^^^^^^^^^^^^^^^

#. Since the ``Job`` model class has ``id`` and ``name`` fields, it too can inherit from ``AbstractEntity``. Update the
   class definition of ``Job`` to extend ``AbstractEntity``. Remove the redundant fields from ``Job``.

#. Replace the type of the field ``employer`` to be of type ``Employer``. You will also need to refactor the affected constructor
   and getter and setter that use this field.

#. Add the ``@ManyToOne`` annotation on the field ``employer``

.. _data-in-homecontroller:

Updating ``HomeController``
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. admonition:: Warning

   As above, there is a test in ``TestTaskThree`` that needs to be uncommented. There is only one, and it is near the end of the file. Do that now.

   Open ``TestTaskThree`` in IntelliJ and find this test.

   #. Select the entire commented-out method.
   #. Uncomment the method by using ``cmd+/`` on Mac or ``ctrl+/`` on Windows.

   If you do not uncomment this test, your code will not pass the autograder.

We’ll make several updates here. Similar to what you have done in Part 1, several of the methods in ``HomeController`` are
missing code because the class has not yet been *wired* with the data layer yet.


#. Add a field ``employerRepository`` annotated with ``@Autowired``.
#. A user will select an employer when they create a job. Add the employer data from ``employerRepository`` into the form template.
   The add job form already includes an employer selection option. Be sure your variable name for the employer data matches that
   already used in ``templates/add``.
#. Checkout ``templates/add.html``. Make a mental note of the name of the variable being used to pass the selected employer
   id on form submission.
#. In ``processAddJobForm``, add code inside of this method to select the employer object that has been chosen to be
   affiliated with the new job. You will need to select the employer using the request parameter you've added to the method.

   .. admonition:: Note

      An employer only needs to be found and set on the new job object if the form data is validated.


Test It with SQL
^^^^^^^^^^^^^^^^

You made a lot of changes! Great work.

Assuming you don’t have any compiler errors, start up your
application. Don’t forget to start your SQL server. Make sure you can
create a new job object from the *Add Jobs* form, selecting a pre-existing employer.

Then, make sure the data has been saved in your job table. You should see a column for
``employer_id``, corresponding to the employer object selected for the new job.

You have changed the architecture of your job table. You will still be able to add a new entry that has an
``employer_id`` column but you'll note that job still has the now defunct ``employer`` column. You can keep your database
clean by removing the job table. It will be recreated when you run the application again.

#. **SQL TASK:** In ``queries.sql`` under "Part 3", write the SQL statement to remove the job table.


The *List* and *Search* functionality still isn't quite fixed so to view a job in the application, make a note
of the job's id in the SQL table. Back in your browser, enter the path for ``/view/{jobId}``.


When everything works, move on to Part 4 below.

.. _tech-jobs-persistent-pt4:

Part 4: Setting Up a Many-to-Many Relationship
----------------------------------------------

Using a many-to-many relationship, we can now use the ``Skill`` object to store a ``Job`` object's skills. At the moment,
a job can have many skills listed as strings. In this section, you'll be tasked with changing this field type to be a list
of skills. Just as a job requires many skills, any skill can be associated with several jobs. With this in mind, you'll also
add a list of jobs as a field onto the skill class.

.. admonition:: Warning

   As before, there are a few tests in ``TestTaskFour`` that have been commented out because they depend on the code you wrote in Part 1. Open ``TestTaskFour`` in IntelliJ and find these tests. For each one:

   #. Select the entire commented-out method.
   #. Uncomment the method by using ``cmd+/`` on Mac or ``ctrl+/`` on Windows.

   If you do not uncomment these tests, your code will not pass the autograder.

``Skill.jobs``
^^^^^^^^^^^^^^

#. In your ``Skill`` class, add a jobs field.

   #. What type should this field be? Initialize it in the field declaration accordingly.
   #. Add a getter and setter for the field.
   #. This field has a many-to-many type relationship with skills. You'll need to add the ``@ManyToMany`` annotation
      with an argument ``mappedBy="skills"`` to configure this mapping.

Refactor ``Job.skills``
^^^^^^^^^^^^^^^^^^^^^^^

#. Update your ``Job`` model class to fit its many-to-many relationship with skills.

   #. ``Job.skills`` already exists. What needs to change and/or be added to map this relationship?

      .. admonition:: Tip

         Be sure to check the whole class for any necessary type updates.


Updating ``HomeController``, Again
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You next need to wire ``HomeController`` with the skills data in order to add skills objects to a new job.
This will look almost precisely like what you have done for employer data above. Refer back to
:ref:`that section <data-in-homecontroller>` to inject the controller with skill data.

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

You now have all the tools in place to re-implement the list and search views from :ref:`tech-jobs-mvc`.

#. In the ``ListController`` class, add fields for ``EmployerRepository`` and ``SkillRepository``, both annotated with
   ``@Autowired``.
#. You'll also need to pass the employer and skill data from those repositories into the view template rendered at ``list/``.
   Add the right ``model.addAttribute(name, value)`` statements to pass this info into ``templates/list.html``.


Test It with SQL
^^^^^^^^^^^^^^^^

Run your application and make sure you can create a new job with an employer and several skills. You should now also have restored
full list and search capabilities.

#. **SQL TASK:** In ``queries.sql`` under "Part 4", write a query to return the names of all skills that are attached to jobs in alphabetical order.
   If a skill does not have a job listed, it should not be
   included in the results of this query.

When everything works, you’re done! Congrats!

Sanity Check
------------

At this point, all autograding tests should be passing. To be sure, right-click on the ``org.launchcode.techjobs.persistent`` package in ``src/test/java`` and select *Run tests in...* If any test fails, evaluate the failure/error message and go back to fix your code.

If a test in `TestCommentedTests` fails, this means that you failed to uncomment one or more tests in either `TestTaskTwo` or `TestTaskFour`. You will need to go back and uncomment the test(s) and make sure they pass.

How to Submit
-------------

To turn in your assignment and get credit, follow the
:ref:`submission instructions <submitting-your-work>`.

