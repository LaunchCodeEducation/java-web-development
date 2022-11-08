Studio: Restaurant Menu Continued
==================================

We began designing and implementing our ``Menu`` and ``MenuItem`` classes in
the :ref:`last studio <classes-studio-part1>`. Let’s continue working on these
classes by adding some methods.

Design
-------

To review, here are the details you have from the restaurant owner:

#. The menu consists of several menu items.
#. Each menu item has a price, description, and category (appetizer,
   main course, or dessert).
#. It should be possible to display whether or not a menu item is new.
#. The app should know when the menu was last updated, so visitors can
   see that the restaurant is constantly changing and adding exciting
   new items.

Based on these details, you need to include some *instance* methods:

#. A way to add and remove menu items from the menu.
#. A way to tell if a menu item is new.
#. A way to tell when the menu was last updated.
#. A way to print out both a single menu item as well as the entire menu.
#. A way to determine whether or not two menu items are equal.

Starting with pen and paper (or your favorite notes application on your
laptop), sketch out the methods that you need to add to these classes. List the
method names and access levels, along with the types of all input and return
parameters. Also, consider whether any methods should be ``static``.

Share Your Design
------------------

Once you have sketched out your methods, pair with a classmate and take turns
presenting your designs. Class design can be subjective, so it’s important to
properly think and talk through your choices before coding.

While your partner is presenting their design, ask questions about why they
made the decisions they did. Consider other use cases that might come up, and
see if their design fits with those.

Implementation
---------------

#. In IntelliJ, open your ``Restaurant Menu`` project. Open the terminal in IntelliJ and create a branch in your repository for your Lesson 4 Studio solution. For the studio, make sure all of your work is in that branch.
#. Within the ``restaurant`` package, add the methods you designed to your ``Menu`` and
   ``MenuItem`` classes.
#. Create a class called ``Restaurant``, and add a
   ``public static void main(String[] args)`` method.
#. Use the ``main`` method to test your classes:

   a. Create several items and add them to a menu.
   b. Print the entire, updated menu to the screen.
   c. Print an individual menu item to the screen.
   d. Delete an item from a menu, then reprint the menu.

Bonus Mission
--------------

If a user tries to add an item that is already on the menu, print a message
that warns the user about the duplicate. Also, prevent the duplicate from
being added to the menu.

Submitting Your Work
---------------------

In the previous studio, you should have created a repository on GitHub for
your restaurant project.

Since you just modified that project in this studio, commit your changes and
push them up to the same repository. However, you must still submit the URL
for your repository on Canvas.
