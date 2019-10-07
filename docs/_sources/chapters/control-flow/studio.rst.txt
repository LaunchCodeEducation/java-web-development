Studio: Control Flow and Collections
=====================================

In this studio, you will write a program to count the number of times each
character occurs in a string and then print the results to the console.

Feel free to prompt the user for a string. However, for the sake of simplicity,
you might want to start by hard-coding some text and storing it in a variable.
For your convenience, here is a quote from the movie *Hidden Figures*:

   If the product of two terms is zero then common sense says at least one of
   the two terms has to be zero to start with. So if you move all the terms
   over to one side, you can put the quadratics into a form that can be
   factored allowing that side of the equation to equal zero. Once you’ve done
   that, it’s pretty straightforward from there.

.. admonition:: Tip

   Remember, you can turn a ``String`` object into an array of characters
   using:

   .. sourcecode:: java

      char[] charactersInString = myString.toCharArray();

Some Items to Ponder Before Starting
-------------------------------------

#. There are multiple ways to approach this task, but one way involves the
   following steps:

   a. Loop through the string one character at a time,
   b. Store and/or update the count for a given character using an appropriate
      data structure.
   c. Loop through the data structure to print the results (one character and its
      count per line).

#. Which type of data structure (``ArrayList``, ``HashMap``, or ``Array``)
   should you use to store character counts? Any can be made to work, but there
   is a BEST choice.
#. You’ll need to *initialize* the counts for the characters in some fashion.
   It’s probably better to do this as you go through the string instead of
   doing so before you loop through it. (*WHY?*)
#. If you need to review how to create a new class, revisit the instructions in
   :ref:`Studio: Area of a Circle <area-of-a-circle-studio>`.
#. Don’t forget to check out the *Bonus Missions* below.

Sample Output
--------------

For the example string above, your output should look something like:

    TODO: Update letter counts based on new quote.

.. sourcecode:: bash

   A: 1
   D: 2
   L: 1
   N: 1
   P: 1
   U: 1
   V: 1
    : 50
   a: 22
   b: 3
   c: 17
   d: 4
   e: 26
   f: 2
   g: 7
   h: 1
   i: 27
   j: 1
   l: 17
   ,: 4
   m: 11
   n: 14
   .: 8
   o: 15
   p: 7
   q: 3
   r: 9
   s: 29
   t: 29
   u: 28
   v: 4
   x: 1

Bonus Missions
---------------

Try these modifications on your code:

#. Prompt the user to enter the string in the command line.
#. Make the character counts case-insensitive.
#. Exclude non-alphabetic characters.

Super Bonus
^^^^^^^^^^^^

Read the string in from a file.

.. admonition:: Note

   This is a hard one. We won’t talk about reading from files in Java in this
   course, so be ready for a tough challenge if you accept this mission.
