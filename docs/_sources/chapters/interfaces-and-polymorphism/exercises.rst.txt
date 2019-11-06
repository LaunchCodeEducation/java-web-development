Exercises: Interfaces and Polymorphism
=======================================

It takes time for new Java coders to recognize the usefulness of interfaces. At
first glance, they do not seem to provide much benefit over extending a base
class, adding instance methods to a class, or overriding a method like
``toString``.

To help overcome this, let's consider a common occurrence---sorting an
``ArrayList`` of objects.

#. If the list contains ``String`` or numerical entries, then sorting the list
   is :ref:`trivial <arraylist-methods>`:

   .. sourcecode:: Java

      Collections.sort(arrayListName);

#. However, if the elements are custom objects (like ``Cat``), then sorting the
   list becomes more complicated. This is because the objects may contain
   multiple fields, each of which could be used as a sorting option. For
   ``Cat`` objects, this could include ``name``, ``age``, or ``mass``.

Getting Started
-----------------

   IntelliJ directions for getting into the lesson 7 package.

We are going to practice with interfaces by playing around with a small ice
cream store. It consists of a refrigerated display ``Case``, which contains
a collection of ice cream ``Flavor`` objects and a selection of ``Cone``
objects.

.. admonition:: Tip

   Did you notice the abstract ``Ingredient`` class? This gets extended into
   ``Flavor`` and ``Cone`` to help streamline the code.

Sorting Flavors by Name
------------------------

To display a menu for the customers, we need to sort the ice cream flavors
alphabetically by their ``name`` field.

For comparison, let's do this without interfaces:



But...

   Ah ha! An exiting interface has solved the sorting-objects-by-field
   problem.

Sorting Cones by Cost
----------------------

Use the ``Comparator`` interface to sort ``cones`` list by cost...
