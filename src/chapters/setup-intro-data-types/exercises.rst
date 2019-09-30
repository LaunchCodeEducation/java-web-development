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
      Preferences > Appearance & Behavior > System Settings* and un-check
      *Reopen last project on startup*. (For Windows users: *File >
      Settings > Appearance & Behavior > System Settings*.) Close and
      Reopen IntelliJ.

#. From the “Welcome to IntelliJ” dialog, select *Check out from Version
   Control > Git*

   .. figure:: figures/IntelliJVCS.png
      :scale: 40%
      :alt: IntelliJ VCS

      IntelliJ VCS

#. Click the button on the lower left corner of the dialog to log in to your
   Github account.

   .. figure:: figures/IntelliJGithub.png
      :scale: 65%
      :alt: IntelliJ Github

      IntelliJ Github

   .. note::

      To work with a remote repository in IntelliJ, you need to configure the
      program to access your GitHub account. We recommend authenticating your
      account using a token. This takes only one brief extra step, and will
      prevent you from having to update IntelliJ settings when you ever change
      your GitHub password.

#. From the URL dropdown options, select your fork of
   ``java-web-dev-exercises``, along with an appropriate source destination
   directory (i.e. a folder where you’ve stored other projects for this class).

   .. figure:: figures/IntelliJRepoSelection.png
      :alt: IntelliJ Repo Selection

      IntelliJ Repo Selection

#. When asked “Would you like to create an IDEA project…” select *Yes*.

   .. figure:: figures/IntelliJAddFileToGit.png
      :scale: 40%
      :alt: IntelliJ Add File To Git

      IntelliJ Add File To Git

#. You'll then be presented with several pages that ask you about other
   settings for your project. Select the *Next* button on all of these pages,
   accepting the default settings.

#. When your project is ready, you'll see a page that looks like the image
   below. Click on the area in the top left labelled *Project*.

   .. figure:: figures/IntelliJNewProject.png
      :scale: 30%
      :alt: IntelliJ New Project

      IntelliJ New Project

#. Clicking on *Project* opens a side panel, displaying the file structure of
   the project you have just set up.

   .. figure:: figures/IntelliJProjectWindow.png
      :scale: 30%
      :alt: IntelliJ Project Window

      IntelliJ Project Window

#. Double-clicking on the *Hello* file opens the file to the right.

   .. figure:: figures/IntelliJOpenFile.png
      :alt: IntelliJ Open File

      IntelliJ Open File

#. To run the *Hello* program, click on the green arrow next to the class
   definition and select *Run 'Hello.main()'* from the dropdown menu.

   .. figure:: figures/IntelliJRunFile.png
      :alt: IntelliJ Run File

      IntelliJ Run File

   After a few seconds, you should see a new window appear with your program's
   output.

   .. figure:: figures/IntelliJFileOutput.png
      :alt: IntelliJ File Output

      IntelliJ File Output

With that, you’re ready to go!

Troubleshooting
---------------

ClassNotFoundException
^^^^^^^^^^^^^^^^^^^^^^

If you experience ``java.lang.ClassNotFoundException`` when trying to
run code after setting up the project, follow these steps:

#. Select *File > Close Project*. If you have any other IntelliJ projects open,
   close them as well.

   .. figure:: figures/closeProject.png
      :scale: 40%
      :alt: Close Project

      Close Project

#. You should see the IntelliJ startup window, click the *X* next to
   ``java-web-dev-exercises`` in the left-hand pane.

   .. figure:: figures/startupWithProject.png
      :scale: 40%
      :alt: Startup with Project

      Startup with Project

#. From the same startup window, select *Import Project* from the right-hand
   pane.

   .. figure:: figures/startupWithoutProject.png
      :scale: 40%
      :alt: Startup without Project

      Startup without Project

#. Follow the steps that IntelliJ guides you through, accepting all defaults.
   When prompted to overwrite IntelliJ settings files, confirm that you want to
   do so.

Instructions
------------

Work on these exercises in the IntelliJ ``java-web-dev-exercises`` project.
Create a new class for each numbered exercise. You may name the classes
whatever you like, but use proper :ref:`naming-conventions` and make sure that
the file name matches the class name.

Creating a Package and Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Here is how to create a new package to store these exercises, and how to
create new classes within this package:

#. Click on the folder ``src`` in the Project pane, then right-click (or
   control-click for some Mac users) and select *New* and then select
   *Package*.

   .. figure:: figures/newPackage.png
      :scale: 30%
      :alt: New Package

      New Package

#. Name the package “exercises”.

   .. figure:: figures/namePackage.png
      :scale: 35%
      :alt: Name Package

      Name Package

#. Right-click/Control-click on the newly created ``exercises`` folder. Select
   *New* and then *Java Class*.

   .. figure:: figures/newClass.png
      :scale: 30%
      :alt: New Class

      New Class

#. Name this what you will name your class (for example, in the 4th exercise
   below, you might name the class ``Alice``).

   .. figure:: figures/nameClass.png
      :scale: 60%
      :alt: Name Class

      Name Class


   .. note::

      You will be asked whether you want to add this file to Git.
      Press the “Yes” button.

   .. figure:: figures/addToGit.png
      :scale: 70%
      :alt: Add class to Git

      Add class to Git

#. You created the new class! You can proceed to write code within
   it. (Don’t forget to write the ``main`` method!)

   .. figure:: figures/newClassCreated.png
      :scale: 30%
      :alt: Ready to start

      Ready to start

Exercises
---------

#. **Input/output**: Write a new “Hello, World” program to prompt the
   user for their name and greet them by name.

   #. Follow steps 3-5 above to create a new ``HelloWorld`` Class inside of
      your ``exercises`` folder.
   #. Add an import statement at the the top of the file to include
      ``Scanner``:

      .. sourcecode:: java

         import java.util.Scanner;

   #. Declare a variable of type ``Scanner`` called ``input``:

      .. sourcecode:: java

         Scanner input = new Scanner(System.in);

   #. Add a question to ask the user:

      .. sourcecode:: java

         System.out.println("Hello, what is your name:");

   #. Create a variable to store the user's response using the ``Scanner``'s ``.nextLine()`` method

      .. sourcecode:: java

         String name = input.nextLine();

   #. Use concatenation to print the greeting:

      .. sourcecode:: java

         System.out.println("Hello " + name);

   #. Right-click/Control-click the arrow next to your class and run the program.


#. **Numeric types**: Write a program to calculate the area of a
   rectangle and print the answer to the console. You should prompt the
   user for the dimensions. (What data types should the dimensions be?)

   #. Follow steps 3-5 above to create a new Class inside of your exercises.
   #. Add an import statement at the top of your file to use ``Scanner``.
   #. Add a ``Scanner`` object to handle the user's input.
   #. Add a print line to prompt the user for the length of the rectangle.
   #. Define a variable to handle the user's response.
      Now is the time to know what type the dimension will be.

      .. tip::

         You'll need to use a different ``Scanner`` method than what we used
         in Exercise 1 above.


   #. Repeat the previous two steps to ask for and store the rectangle's width.
   #. Use the length and width values to calculate the rectangle's area.
   #. Print a statement using concatenation to communicate to the user what the area of
      their rectangle is.
   #. Run the program to verify your code.

#. **Numeric types**: Write a program that asks a user for the number of
   miles they have driven and the amount of gas they’ve consumed (in
   gallons), and print their miles-per-gallon.
#. **Strings**: The first sentence of *Alice’s Adventures in Wonderland*
   is below. Store this sentence in a string, and then prompt the user
   for a term to search for within this string. Print whether or not the
   search term was found. Make the search case-insensitive, so that searching
   for “alice”, for example, prints ``true``.

      ``Alice was beginning to get very tired of sitting by her sister on the
      bank, and of having nothing to do: once or twice she had peeped into the
      book her sister was reading, but it had no pictures or conversations in
      it, 'and what is the use of a book,' thought Alice 'without pictures or
      conversation?'``

#. **Strings**: Extend the previous exercise. If the user enters a word that is
   in the sentence, print out its index within the string and its length. Next,
   remove the word from the string and print the sentence again to confirm your
   code. Remember that strings are *immutable*, so you will need to reassign
   the old sentence variable or create a new one to store the updated phrase.
