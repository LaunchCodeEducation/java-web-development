Exercises: Data Types
======================

Initial Setup
-------------

The steps here will walk you through setting up a repository that you’ll
use to study example code, work on studios, and complete your first
assignment of this unit.

#. Create a *Fork* of `LaunchCodeEducation/java-web-dev-exercises <https://github.com/LaunchCodeEducation/java-web-dev-exercises>`__.
   Do not clone and create a local version of this repo just yet. 
   
#. Open IntelliJ.

   .. note::

      If the app opens up to an existing project, select *IntelliJ >
      Preferences > Appearance & Behavior > System Settings* and uncheck
      *Reopen last project on startup*. (For Windows users: *File >
      Settings > Appearance & Behavior > System Settings*.) Close and
      Reopen IntelliJ.

#. From the “Welcome to IntelliJ” dialog, select *Check out from Version
   Control > Git*
   **TODO: Get screenshots of this process.**
#. Click the button on the lower left corner of the dialog to configure your Github account.
#. To work with a remote repository in IntelliJ, you need to configure the program to access 
   your GitHub account. We recommend taking the extra step of authenticating using a token. 
   This takes only one brief extra step, and will prevent you from having to update IntelliJ
   settings when you ever change your GitHub password.
#. From the URL dropdown options, select your fork of ``java-web-dev-exercises``, 
   along with an appropriate source destination directory (i.e. a folder where you’ve stored other projects for this class).
#. When asked “Would you like to create an IDEA project…” select *Yes*, 
   and then accept all of the default options that are presented.

With that, you’re ready to go!

Here’s a video walking through the last 4 steps above:

.. raw:: html

   <iframe width="560" height="315" src="https://www.youtube.com/embed/OPCaYVXRm_c" frameborder="0" allowfullscreen></iframe>



Troubleshooting
---------------

ClassNotFoundException
^^^^^^^^^^^^^^^^^^^^^^

If you experience ``java.lang.ClassNotFoundException`` when trying to
run code after setting up the project, follow these steps: 

#. Select *File > Close Project*. If you have any other IntelliJ projects open,
   close them as well.

   .. figure:: figures/closeProject.png
      :alt: Close Project

      Close Project

#. You should see the IntelliJ startup window, click the *X* next to 
   ``java-web-dev-exercises`` in the left-hand pane.

   .. figure:: figures/startupWithProject.png
      :alt: Startup with Project

      Startup with Project

#. From the same modal window, select *Import Project* from the right-hand pane.

   .. figure:: figures/startupWithoutProject.png
      :alt: Startup without Project

      Startup without Project

#. Follow the steps that IntelliJ guides you through, accepting all defaults. When prompted to overwrite IntelliJ settings files, confirm that you want to do so.


Instructions
------------

Work on these exercises in the IntelliJ ``java-web-dev-exercises`` project. Create a
new class for each numbered exercise. You may name the classes whatever you like, but use
proper :ref:`naming-conventions` and make sure that the file name matches the class name.

Creating a Package and Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Here is how to create a new package to store these exercises, and how to
create new classes within this package:

#. Click on the folder ``src`` in the Project pane, then right click and
   select *New* and then select *Package*.

   .. figure:: figures/newPackage.png
      :alt: New Package

      New Package

#. Name the package “exercises”.

   .. figure:: figures/namePackage.png
      :alt: Name Package

      Name Package

#. Right-click on the newly created exercises folder. Select *New* and then *Java Class*.

   .. figure:: figures/newClass.png
      :alt: New Class

      New Class

#. Name this what you will name your class (for example, in the
   4th exercise below, you might name the class ``Alice``).

   .. figure:: figures/nameClass.png
      :alt: Name Class

      Name Class


   .. note:: 
      You will be asked whether you want to add this file to Git.
      Press the “Yes” button.
   
   .. figure:: figures/addToGit.png
      :alt: Add class to Git

      Add class to Git

5. The new class is now created! You can proceed to write code within
   it. (Don’t forget to write the ``main`` method!)

   .. figure:: figures/newClassCreated.png
      :alt: Ready to start

      Ready to start

Exercises
---------

1. **Input/output**: Write a new “Hello, World” program to prompt the
   user for their name and greet them by name.
2. **Numeric types**: Write a program to calculate the area of a
   rectangle and print the answer to the console. You should prompt the
   user for the dimensions. (What data types should the dimensions be?)
3. **Numeric types**: Write a program that asks a user for the number of
   miles they have driven and the amount of gas they’ve consumed (in
   gallons), and print their miles-per-gallon.
4. **Strings**: The first sentence of *Alice’s Adventures in Wonderland*
   is below. Store this sentence in a string, and then prompt the user
   for a term to search for within this string. Print whether or not the
   search term was found. See if you can make the search
   case-insensitive, so that searching for “alice”, for example, prints ``true``.

      ``Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, 'and what is the use of a book,' thought Alice 'without pictures or conversation?'``
