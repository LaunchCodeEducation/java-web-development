Exercises: Interfaces and Polymorphism
=======================================

It takes time for new Java coders to recognize the usefulness of interfaces. At
first glance, they do not seem to provide much benefit over extending a base
class, adding instance methods to a class, or overriding a method like
``toString``.

To help overcome this, let's consider a common occurrence---sorting an
``ArrayList`` of objects.

If the list contains ``String`` or numerical entries, then sorting the list
is trivial:

.. sourcecode:: Java

   Collections.sort(listName);

However, if the elements are custom objects (like ``Cat``) then sorting the
list becomes more complicated. This is because the objects contain multiple
fields, each of which could be used as a sorting option. For ``Cat`` objects,
this could include ``name`` or ``age``.

Getting Started
-----------------

   IntelliJ directions for getting into the lesson 7 package.

Sorting Flavors by Name
------------------------

Sort ``flavors`` array by name... (steps walk through how to do this).

But...

   Ah ha! An exiting interface has solved the sorting-objects-by-field
   problem.

Sorting Cones by Cost
----------------------

Use the ``Comparator`` interface to sort ``cones`` list by cost...
