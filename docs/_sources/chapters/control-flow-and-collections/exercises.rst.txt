Exercises: Control Flow and Collections
========================================

Work on these exercises in the IntelliJ ``java-web-dev-exercises`` project,
creating a new class for each item. You may call these classes whatever you
like, but remember to use the proper
:ref:`Java naming conventions <naming-conventions>`.

Array Practice
---------------

#. Create and initialize an array with the following values in a single line:
   ``1, 1, 2, 3, 5, 8``.
#. Loop through the array and print out each value, then modify the loop to
   only print the odd numbers.
#. For this exercise, use the string ``I would not, could not, in a box. I
   would not, could not with a fox. I will not eat them in a house. I will not
   eat them with a mouse.`` Use the ``split`` method to divide the string at
   each space and store the individual words in an array. If you need to review
   the method syntax, look back at the :ref:`String methods <string-methods>`
   table.
#. Print the array of words to verify that your code works. The syntax is:

   .. sourcecode:: java

      System.out.println(Arrays.toString(arrayName));

#. Repeat steps 3 and 4, but change the delimiter to split the string into
   separate sentences.

.. admonition:: Note

   Some characters, like a period ``"."``, have special meanings when used with
   the ``split`` method. They cannot be used as-is for the deliminator.

   To use these characters as the deliminator, we must *escape* their special
   meanings. Instead of ``.split(".")``, we need to use ``.split("\\.")``.

ArrayList Practice
-------------------

#. Write a static method to find the sum of all the even numbers in an
   ArrayList. Within ``main``, create a list with at least 10 integers and call
   your method on the list.
#. Write a static method to print out each word in a list that has exactly 5
   letters.
#. Modify your code to prompt the user to enter the word length for the search.
#. BONUS: Instead of creating our own list of words, what if we want to use the
   string from the *Array Practice* section? Search "Java convert String to
   ArrayList" online to see how to split a string into the more flexible
   ``ArrayList`` collection.

HashMap Practice
-----------------

Make a program similar to ``GradebookHashMap`` that does the following:

#. It takes in student names and ID numbers (as integers) instead of names and
   grades.
#. The keys should be the IDs and the values should be the names.
#. Modify the roster printing code accordingly.
