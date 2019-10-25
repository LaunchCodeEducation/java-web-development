Assignment #2: Revised Tech Jobs (Object-Oriented Edition)
===========================================================

Introduction
------------

Your apprenticeship at LaunchCode is going well! Only a few weeks in and you’re
regularly making contributions to code that will eventually be used by all
LaunchCode staff.

Your last task was to get the prototype Tech Jobs app in good shape. Now it’s
time to advance the underlying structure of the program.

Your mentor on this project is Sally, one of the developers at LaunchCode. She
regularly supports coders who are just getting started with their careers.

.. figure:: figures/LC-Sally.png
   :scale: 50%
   :alt: Sally's LaunchCode avatar.

After seeing your strong work with your last project, Blake reported that you
performed well and learned quickly. Because of your success, he and Sally feel
comfortable assigning you to a set of tasks that are a notch up in difficulty.

Sally completed some initial work on the project and left you some TODOs.

Learning Objectives
--------------------

In this project, you’ll show that you can:

#. Read and understand code written by others.
#. Work with *objects* to encapsulate data and methods.
#. Use the generator in IntelliJ to automate routine tasks.
#. Use unit testing and Test-Driven-Development (TDD) to verify and create new
   methods.
#. Apply the concept of inheritance to streamline your classes (the DRY
   idea---Don't Repeat Yourself).

Get the Starter Code
---------------------

   TODO: Add link to new starter code for TechJobs-OO.

.. TODO: Add link to new starter code for TechJobs OO

#. Set up a local copy of the project. Visit the repository page for this
   project and fork the repo to create a copy in your own GitHub account.
#. Open IntelliJ (if IntelliJ is currently open, save your work, close it, and
   reopen it).
#. If the app opens up to an existing project, select *IntelliJ > Preferences >
   Appearance & Behavior > System Settings* and uncheck *Reopen last project on
   startup*. Close and Reopen IntelliJ.
#. From the “Welcome to IntelliJ” dialog box, select *Check out from Version
   Control > Git*.
#. Choose your fork from the repository dropdown, select the parent directory
   where you’d like to store your project, and hit *Clone*.
#. In the screens that follow:

   a. Choose *Create Project From Existing Sources* on the first pane.
   b. Select the defaults in all the other panes.

TechJobs (Object-Oriented Edition)
-----------------------------------

Sally has gotten the ball rolling by adding a ``Job`` class, along with classes
to represent the individual properties of a job: ``Employer``, ``Location``,
``PositionType``, and ``CoreCompetency``. She completed the ``Employer`` class,
and she left you the task of filling in the others.

Sally also refactored the display methods to use these new classes. Finally,
she modified the ``JobData`` class to properly create ``Job`` and related
objects when importing data from ``job_data.csv``.

As the team gets closer to deploying the app---and abandoning the test data
they’ve been using---they’ll want an easy way to add and remove jobs via a
user interface. Before that, however, you need to finish shifting the project
to an object-oriented design.

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

If you don’t have it open already, open the ``Job`` class. You’ll see the
following fields (among others):

.. sourcecode:: java
   :linenos:

   private String name;
   private Employer employer;
   private Location location;
   private PositionType positionType;
   private CoreCompetency coreCompetency;

Of these, only ``name`` is a string. Sally created classes to represent each of
the other properties. Each of these classes---``Employer``, ``Location``,
``CoreCompetency``, ``PositionType``---have ``value`` and ``id`` fields.

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
represents that company.

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

You’ve been assigned the following tasks:

#. Review Sally's code in the ``Employer`` class to learn how to assign a
   unique ID.
#. Add getters, setters, and custom methods as needed to the ``Location``,
   ``CoreCompetency``, and ``PositionType`` classes.
#. Complete the ``Job`` class using what you learned in steps 1 and 2.
#. Refactor the ``printJobs`` method to use ``Job`` objects.
#. Use unit testing to verify the ID generator and ``equals`` methods.
#. Use TDD to design and code a custom ``toString`` method.
#. Use inheritance to DRY the code within ``Employer``, ``Location``,
   ``CoreCompetency``, and ``PositionType``.

1) Explore the ``Employer`` Class
----------------------------------

Open the ``Employer`` file in IntelliJ and examine the code. In addition to the
two fields---``id`` and ``value``---the class includes the standard getters and
setters as well as some custom methods like ``toString`` and ``equals``.

You can refer to these examples as you fill in the missing pieces in the other
classes, but for now let's take a closer look at the constructors.

Assign a Unique ID
^^^^^^^^^^^^^^^^^^^

One neat trick we can use is to automatically assign each new object a unique
ID number.

.. admonition:: Example

   Examine the two constructors in ``Employer.java``:

   .. sourcecode:: java
      :linenos:

      public class Employer {
         private int id;
         private static int nextId = 1;
         private String value;

         public Employer() {
            id = nextId;
            nextId++;
         }

         public Employer(String aValue) {
            this();
            this.value = aValue;
         }

         // Getters and Setters omitted from this view.
      }

#. Line 3 declares the variable ``nextId``. Since it is ``static``, its
   changing value is NOT stored within any ``Employer`` object.
#. The first constructor (lines 6 - 9) accepts no arguments and assigns the
   value of ``nextId`` to the ``id`` field. It then increments ``nextId``.
   Thus, every new ``Employer`` object will get a different ID number.
#. The second constructor (lines 11 - 14) assigns ``aValue`` to the ``value``
   field. However, it ALSO initializes ``id`` for the object by calling the
   first constructor with the ``this();`` statement. Including ``this();`` in
   any ``Employer`` constructor makes initializing ``id`` a default behavior.

2) Complete the Support Classes
--------------------------------

Sally needs you to build up the remaining classes. In each case, you can refer
to the ``Employer`` class for hints on how to structure your code.

The ``Location`` Class
^^^^^^^^^^^^^^^^^^^^^^^

Open the ``Location.java`` file. Note that the getters, setters, and custom
methods for this class are done, as is the constructor for initializing the
``id`` field.

Sally left you a ``TODO`` comment with instructions for coding a second
constructor:

#. It should call the first constructor to initialize the ``id`` field.
#. It must also initialize the ``value`` field for a new ``Location`` object.

The ``CoreCompetency`` Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open the class file. In this case, the constructors and custom methods are
ready. Sally needs you to complete the somewhat tedious task of writing the
getters and setters for the ``id`` and ``value`` fields, but NOT for
``nextID``.

Fortunately, IntelliJ has a tool to help with this:

#. Right-click in the editor pane and select *Generate*.
#. Select the *Getter and Setter* option.
#. Select the ``id`` and ``value`` options, then click *OK*.

PRESTO! Getters and setters appear.

The ``PositionType`` Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open the class file. This time the constructors, getters, and setters are done.
Sally's comments direct you to where you need to add the custom methods.

#. Code a ``toString`` method that just returns the value of a ``PositionType``
   object.
#. Use the *Generate* option again to add the ``equals`` and ``hashCode``
   methods. Refer to the :ref:`previous section <equals-shortcut>` of this
   chapter if you need a quick review.
#. Assume that two ``PositionType`` objects are equal when their ``id`` fields
   match.

.. admonition:: Tip

   Now would be a good time to save, commit, and push your work up to GitHub.

3) Complete the ``Job`` Class
------------------------------

Now open the ``Job`` file. OOF! There are a lot of fields declared and not much
else.

#. Code a constructor to initialize the ``id`` field with a unique value. This
   constructor should take no parameters.
#. Code a second constructor that takes 5 parameters and assigns values to
   ``name``, ``employer``, ``location``, ``positionType``, and
   ``coreCompetency``. Also, this constructor should call the first in order to
   initialize the ``id`` field.
#. Generate getters and setters for each field EXCEPT ``id`` and ``nextID``.
   For the ``id`` field, just generate a getter.
#. Generate the ``equals`` and ``hashCode`` methods. Consider two ``Job``
   objects equal when their id fields match.

The ``Main`` file contains code to create two ``Job`` objects and then print
their field values. Run the ``main`` method to verify that you set up your
classes correctly.

.. admonition:: Tip

   Save, commit, and push your work to GitHub.

4) Refactor ``printJobs``
--------------------------

5) Use Unit Testing to Verify Parts of the ``Job`` Class
---------------------------------------------------------

6) Use TDD to Build The ``toString`` Method
---------------------------------------------

Create Tests for ``toString``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Code ``toString`` to Pass
^^^^^^^^^^^^^^^^^^^^^^^^^^^

7) Refactor to DRY the Support Classes
---------------------------------------

Create a Base ``JobFields`` Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Extend ``JobFields`` into Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Remove Extraneous Code
^^^^^^^^^^^^^^^^^^^^^^^

How to Submit
--------------

To turn in your assignment and get credit, follow the
:ref:`submission instructions <how-to-submit-work>`.


Fill in small fields.
Fill out Job class.
Refactoring JobData class.
Testing... ID generator, .equals.
TDD to build toString method.
Refactor classes to use inheritance.
