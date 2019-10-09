.. _area-of-a-circle-studio:

Studio: Area of a Circle
========================

Get cosy with Java syntax by writing a console program that calculates the
area of a circle based on input from the user.

Creating your class
-------------------

Since you’re still new to Java and IntelliJ, we’ll provide some extra
direction the first few coding exercises.

First, make a new folder, or package, to hold your studio exercises. Create a
new package named ``org.launchcode.java.studios.areaofacircle`` by
right-clicking (or ctrl-clicking for some Mac users) on the ``src`` directory
in ``java-web-dev-exercises`` and selecting *New > Package*. Be sure to enter
the full name, or your package won’t be created in the correct location.

Create your class in the ``java-web-dev-exercises`` project within the
package ``org.launchcode.java.studios.areaofacircle`` by
right-clicking/ctrl-clicking on the ``studios.areaofacircle`` package/folder
and selecting *New > Java Class*. Enter the name ``Area``. Select the option
to add the file to Git when the window appears.

Your first task
---------------

Write a class, ``Area``, that prompts the user for the radius of a circle and
then calculate its area and print the result.

.. admonition:: Tip

   Recall that the area of a circle is ``A = pi * r * r`` where ``pi`` is
   3.14 and ``r`` is the radius.

.. note::

   Unlike some other languages, Java does not have an exponent operator.


Here’s an example of how your program should work:

::

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

Your next task
--------------

Add a second Java file to your program to delegate the area calculation away
from the printing task.

#. Add a new class in your ``studios.areaofacircle`` package called ``Circle``.
#. Create a method called ``getArea`` inside of ``Circle`` that takes a Double
   ``radius`` as its only parameter and returns another ``Double``, the result of
   the area calculation.

   .. sourcecode:: java

      public static Double getArea(Double radius) {
        return 3.14 * radius * radius;
      }

#. Back in ``Area``, replace your area calculation line with a call to
   ``Circle.getArea()``.

   .. tip::

      Check out the ``HelloMethods`` and ``Message`` example from
      :ref:`static-methods` for a reference on how to use a class from another
      file.

Bonus Missions
--------------

1. Add validation to your program. If the user enters a negative number? a
   non-numeric character? the empty string? Print an error message and quit.
   You’ll need to peek ahead to learn
   about `conditional syntax in
   Java <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/if.html>`__.
2. Extend your program further by using a `while or do-while
   loop <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/while.html>`__,
   so that when the user enters a negative number they are re-prompted.
