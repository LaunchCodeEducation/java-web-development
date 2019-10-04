Studio: Control Flow to Count Characters
=========================================

In this studio, you will write a program to count the number of times each
character occurs in a string and then print the results to the console.

You could prompt the user for a string, but for the sake of simplicity, you can
start by hard-coding the string and storing it in a variable. Here’s a test
string, for your convenience:

   TODO: Decide which of these to use.

   Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc accumsan sem
   ut ligula scelerisque sollicitudin. Ut at sagittis augue. Praesent quis
   rhoncus justo. Aliquam erat volutpat. Donec sit amet suscipit metus, non
   lobortis massa. Vestibulum augue ex, dapibus ac suscipit vel, volutpat eget
   massa. Donec nec velit non ligula efficitur luctus.

   Twas brillig, and the slithy toves
   Did gyre and gimble in the wabe:
   All mimsy were the borogoves,
   And the mome raths outgrabe.
   Beware the Jabberwock, my son!
   The jaws that bite, the claws that catch!
   Beware the Jubjub bird, and shun
   The frumious Bandersnatch!

There are multiple ways to approach this task, but one way involves the
following steps:

#. Loop through the string one character at a time,
#. Store and/or update the count for a given character using an appropriate
   data structure.
#. Loop through the data structure to print the results (one character and its
   count per line).

.. admonition:: Tip

   You can turn a ``String`` object into an array of characters using:

   .. sourcecode:: java

      char[] charactersInString = myString.toCharArray();

Some Items to Ponder Before Starting
-------------------------------------

#. Which type of data structure (``ArrayList``, ``HashMap``, or ``Array``)
   should you use to store character counts? Any can be made to work, but there
   is a BEST choice.
#. You’ll need to “initialize” the counts for the characters in some fashion.
   It’s probably better to do this as you go through the string, as opposed to
   doing so before you loop through the string. (*WHY?*)
#. If you need to review how to create a new class, revisit the instructions in
   `Studio: Area of a Circle <../area/>`__.
#. Don’t forget to check out the *Bonus Missions* below.

Sample Output
--------------

For the example string above, your output should look something like:

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

Here are few ways you might modify your solution:

#. Prompt the user to enter the string in the command line.
#. Make the character counts case-insensitive.
#. Exclude non-alphabetic characters.

Super Bonus
^^^^^^^^^^^^

Read the string in from a file.

*Note:* This is a hard one. We won’t talk about reading from files in Java in
this course, so be ready for a tough challenge if you accept this mission.
