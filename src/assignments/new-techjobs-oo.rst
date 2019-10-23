Assignment #2: Tech Jobs (Object-Oriented Edition)
===================================================

Introduction
------------

Your apprenticeship at LaunchCode is going well! Only a few weeks in and you’re
regularly making contributions to code that will eventually be used by all
LaunchCode staff.

Your last task was to get the prototype Tech Jobs app in good shape. Now it’s
time to advance the underlying structure of the program.

Your mentor on this project is Sally, one of the developers at LaunchCode. She
regularly supports developers who are just getting started with their careers.

.. figure:: figures/LC-Sally.png
   :scale: 50%
   :alt: Sally's LaunchCode avatar.

She’s done some initial work on the project and left you some TODOs. After
seeing your strong work with your last project, Blake reported that you
performed well and learned quickly. Because of your success, he and Sally feel
comfortable assigning you to a set of tasks that are a notch up in difficulty.

Learning Objectives
--------------------

In this project, you’ll show that you can:

#. Read and understand code written by others.
#. Work with *objects* to encapsulate data and methods.
#. Use the generator in IntelliJ to automate routine tasks.
#. Use unit testing and TDD to create new methods.

Get the Starter Code
---------------------

.. TODO: Add link to new starter code for TechJobs OO

#. Set up a local copy of the project: Visit the repository page *(TODO: Add
   link)* for this project and fork the repository to create a copy in your
   own GitHub account.
#. Open IntelliJ (if IntelliJ is currently open, save your work, close it, and
   reopen it).
#. If the app opens up to an existing project, select *IntelliJ > Preferences >
   Appearance & Behavior > System Settings* and uncheck *Reopen last project on
   startup*. Close and Reopen IntelliJ.
#. From the “Welcome to IntelliJ” dialog box, select *Check out from Version
   Control > GitHub*.
#. Choose your fork from the repository dropdown, select the parent directory
   where you’d like to store your project, and hit *Clone*.
#. In the screens that follow:

   a. Choose *Create Project From Existing Sources* on the first pane.
   b. Select *Auto Import* in the Gradle configuration pane.
   c. Select defaults on all other panes

TechJobs (Object-Oriented Edition)
-----------------------------------

Sally has gotten the ball rolling by adding a ``Job`` class, along with classes
to represent the individual properties of a job: ``Employer``, ``Location``,
``PositionType``, and ``CoreCompetency``.

She also refactored the display methods to use these new classes. Finally, she
modified the ``JobData`` class to properly create ``Job`` and related objects
when importing data from ``job_data.csv``.

As the team gets closer to deploying the app---and abandoning the test data
they’ve been using---they’ll want an easy way to add and remove jobs via a
user interface.

Why Change to Object-Oriented?
-------------------------------

Working with data stored as strings in HashMaps and ArrayLists isn’t a good
long-term solution, for reasons that we point out below.

The ``Job`` class introduces an object-oriented design to the application. It
contains all of the fields you used in the console version of TechJobs:
``name``, ``employer``, ``location``, ``positionType``, ``coreCompetency``.
There’s also an ``id`` field which will be used to uniquely identify ``Job``
objects.

The main difference between the object representation of a job and the
string-based representation is that the values of ``employer``, ``location``,
and the other non-ID fields are no longer strings. Instead, they are classes of
their own.

Job Fields
^^^^^^^^^^^

If you don’t have it open already, open the ``Job`` class. You’ll see
the following fields (among others):

.. sourcecode:: java
   :linenos:

   private String name;
   private Employer employer;
   private Location location;
   private PositionType positionType;
   private CoreCompetency coreCompetency;

Of these, only ``name`` is a string. Sally has created classes to represent
each of the other properties. Each of these classes---``Employer``,
``Location``, ``CoreCompetency``, ``PositionType``---have ``value`` and ``id``
fields.

So, for example, if you had a ``Job`` instance, you could get the name of the
employer this way:

.. sourcecode:: java

   // job is an instance of Job
   String employerName = job.getEmployer().getValue();

Additionally, the ``toString()`` method of the ``Employer`` class is set up to
return the ``value`` field. Thus, using one of these objects in another string
context like ``System.out.println`` will print the ``value``.

.. sourcecode:: java

   // Prints the name of the employer
   System.out.println(job.getEmployer);

Why do we go to all of this trouble, when we could store this job-related data
as strings? There are a couple of reasons.

Eliminate Duplication of Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In our app, we have multiple jobs that have the same value in a given field.
For example, there are multiple jobs with position type “Web - Full Stack”, and
there are different jobs with the same employer. If we store the values of
these fields as strings directly within the ``Job`` class, these strings would
be repeated in several places across the application.

By using objects, we can have a single ``PositionType`` object with value “Web
- Full Stack”. Each job that wants to use that position type holds onto a
reference to the given object. Similarly, we can have one ``Employer`` object
for each employer.

Aside from reducing the amount of raw data / memory that the application uses,
this will allow data to be updated more easily and properly. If we need to
change the name of an employer (e.g. due to a typo or a name change at the
company), we can change it in one place---the single ``Employer`` object that
represents that employer.

Enable Extension
~~~~~~~~~~~~~~~~~

While the four ``Job`` properties represented by objects will primarily be used
for their string values, it’s easy to imagine adding new properties to address
future needs.

For example, it would be useful for an ``Employer`` object to have an address,
a primary contact, and a list of jobs available at that employer.

For a ``Location`` object, it would be useful to have a list of zip codes
associated with that location, in order to determine which location an employer
or job is located in.

If we were to store these properties as strings, extending and modifying this
behavior would be much more complicated and difficult moving forward.

Your Assignment
---------------

You’ve been tasked with completing the following tasks:

#. Add getters, setters, and ``toString`` methods as needed to the new classes.
#. Add custom ``equals`` and ``hashCode`` methods to the ``Job`` class.
#. Code a feature that allows new ``Job`` objects to be added to the system.
#. Use unit testing to verify the add job method.
#. Use Test-Driven-Development (TDD) to design and code a ``removeJob`` method.

A) Complete New Classes
------------------------

B) Code ``addJob`` Method
--------------------------

C) Test ``addJob`` Method
--------------------------

D) Design ``removeJob`` (TDD)
------------------------------

Code Tests for ``removeJob``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Code ``removeJob`` to Pass
^^^^^^^^^^^^^^^^^^^^^^^^^^^

How to Submit
--------------

To turn in your assignment and get credit, follow the
:ref:`submission instructions <how-to-submit-work>`.
