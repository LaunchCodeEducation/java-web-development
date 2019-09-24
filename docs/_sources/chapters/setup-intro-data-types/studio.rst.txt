Studio: Data Types
===================

Get cosy with Java syntax by writing a console program that calculates the 
area of a circle based on input from the user.

Creating your class
-------------------

Since you’re still new to Java and IntelliJ, we’ll provide some extra
direction the first few times we go to write code.

Create a new package named ``org.launchcode.java.studios`` by
right-clicking (or ctrl-clicking for some Mac users) on the ``src`` directory 
in ``java-web-dev-exercises`` and selecting *New > Package*. Be sure to enter 
the full name, or your package won’t be created in the correct location.

Create your program/class in the ``java-web-dev-exercises`` project within the
package ``org.launchcode.java.studios`` by right-clicking/ctrl-clicking on the
``studios`` package/folder and selecting *New > Java Class*. Enter the
name ``Area``. Select the option to add the file to Git when the window appears.

Your task
---------

Write a program/class ``Area`` that prompts the user for a number, and
then calculate the area of a circle with that radius and print the
result.

.. admonition:: Tip
   
   Recall that the area of a circle is ``A = pi * r * r`` where ``pi`` is
   3.14 and ``r`` is the radius.


Here’s an example of how your program should work:

.. sourcecode:: java

   Enter a radius: 2.5
   The area of a circle of radius 2.5 is: 19.625

Some questions to ask yourself: 

#. What data type should the radius be? 
#. What is the best way to get user input into a variable ``radius`` of
   that type?

.. admonition:: Warning

   Be sure to create a ``main`` method to place your code within. It’s
   signature *must* be:

   .. sourcecode:: java

      public static void main(String[] args)


Bonus Missions
--------------

1. Add validation to your program. If the user enters a negative number,
   print an error message and quit. You’ll need to peek ahead to learn
   about `conditional syntax in
   Java <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/if.html>`__.
2. Extend your program further by using a `while or do-while
   loop <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/while.html>`__,
   so that when the user enters a negative number they are re-prompted.
