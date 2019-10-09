Exercises: Data Types
======================

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

#. Name the package "exercises".

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
      Press the "Yes" button.

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

#. **Input/output**: Write a new "Hello, World" program to prompt the
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
   for "alice", for example, prints ``true``.

      ``Alice was beginning to get very tired of sitting by her sister on the
      bank, and of having nothing to do: once or twice she had peeped into the
      book her sister was reading, but it had no pictures or conversations in
      it, 'and what is the use of a book,' thought Alice 'without pictures or
      conversation?'``
   
   .. note::

      You may want to write the string above on more than one line in
      your solution. Java 13 and IntelliJ gives you a few options to do so.
      The easiest, thanks to your IDE, is to press *Enter* as you type the string.
      IntelliJ will close the string and concatenate it with the next line to create
      one longer string.

#. **Strings**: Extend the previous exercise. Assume the user enters a word that is
   in the sentence. Print out its index within the string and its length. Next,
   remove the word from the string and print the sentence again to confirm your
   code. Remember that strings are *immutable*, so you will need to reassign
   the old sentence variable or create a new one to store the updated phrase.
