Updating Past Work
===================

As you complete more and more projects, at some point you will look back at
your early work and think, *Whoa! There is SUCH a better way to do that!* You
will spot places where your old code is inefficient, fragile, or contains a
bug.

No worries! This happens to all developers as our skills advance. We spot
places where our old code could be streamlined or strengthened.

.. admonition:: Examples

   Assume your past-self created a method to check if every integer in an
   ArrayList is identical. Later, your more experienced self tackles the same
   problem.

   **Earlier self**:

   .. sourcecode:: Java
      :linenos:

      private static boolean checkIdentical(ArrayList<Integer> arr){
         int firstNum = arr.get(0);
         boolean identical = true;

         for (int num : arr){
            if (num != firstNum){
               identical = false;
            }
         }

         return identical;
      }

   This code compares the first number in the array to every other value. It
   works, but it's not very efficient.

   **Current self**:

   .. sourcecode:: Java
      :linenos:

      private static boolean checkIdentical(ArrayList<Integer> arr){

         return Collections.min(arr) == Collections.max(arr);

      }

   Bam! One line, no loop. You rock!

Refactoring Code
-----------------

Rather than feeling sheepish about the earliest code you generated, you can
always go back and make updates.

.. index:: ! refactor

**Refactoring** occurs when you improve your old work without adding any new
features. This process is NOT the same as debugging, since your old code runs
just fine. Instead, refactoring makes your code shorter, more efficient, more
flexible, more robust, or more pretty.

One simple example of refactoring involves changing the appearance of a view.
Altering the font, text size, table formatting, or background color does not
make the page behave any differently. However, it would make the view more
appealing to look at.

(If this seems like a trivial change, speak to your nearest marketing person).

Bootstrap
----------

Text here...

Image of standard HTML buttons (boring).

Same buttons with Bootstrap classes.

Image of standard HTML table (boring).

Sample tables with different Bootstrap styling.

Link to Bootstrap documentation.

Adding Bootstrap to your templates. (Best place is in head fragment).

In the video, the Bootstrap classes ``container``, ``form-group``, and
``form-control`` are used to improve the look and feel of the views.

Adding Generic Code
--------------------

.. index:: ! boilerplate code

From time to time, you will see the term **boilerplate code**. This refers to
generic, ready-made code that you can paste into just about any class or
template. Usually, you quickly modify this code to better fit your project,
but the boilerplate statements fill in some of the tedious structure and
routine commands. This saves you time and allows you to focus on the more
interesting parts of your work.

In the second :ref:`Classes and Objects chapter <equals-shortcut>` as well as
in :ref:`Assignment #2 <generator-shortcut>`, you used the IntelliJ *Generate*
shortcut to insert getters, setters, and custom methods into your Java classes.

The *Generate* shortcut can also be used to quickly format class constructors,
which is especially useful if you have declared many field variables.

.. figure:: figures/generateConstructorMenu.png
   :alt: Generate menu options.

Note that when you select *Generate --> Constructor*, you will be able to
select which fields to add to the constructor.

Adding a Default Constructor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Lorem ipsum...

Try It!
--------

Code along with the video below as you refactor your ``coding-events`` project.
You will add a model to deal with the event data, and you will revise the
templates to work with event objects.

.. todo:: Add model video #1 here...

Remember that the reading in this chapter supports the work you complete as you
watch the videos. The text is NOT meant as a replacement for that practice
time.
