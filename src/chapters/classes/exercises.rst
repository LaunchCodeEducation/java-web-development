.. _classes-exercises-part1:

Exercises: Classes and Objects
==============================

Work on these exercises in the IntelliJ ``java-web-dev-exercises`` project.

#. Open up the file, ``Student.java``, and add all of the necessary getters and
   setters. Think about the access level each field and method should have, and
   try reducing the access level of at least one setter to less than public.
#. Instantiate the ``Student`` class using yourself as the student. For the
   ``numberOfCredits`` give yourself ``1`` for this class and a GPA of ``4.0``
   because you are a Java superstar!
#. In the ``school`` package, create a class ``Course`` with at least three
   fields. Before diving into IntelliJ, try using pen and paper to work through
   what these might be. At least one of your fields should be an ``ArrayList``
   or ``HashMap``, and you should use your ``Student`` class.
#. In the ``school`` package, create a class ``Teacher`` with four fields:
   ``firstName``, ``lastName``, ``subject``, and ``yearsTeaching``. Add getters
   and setters to the class and add the access level to each field and method
   in the class. When adding your getters and setters, think about what we read
   about in the section on Encapsulation.

   a. What access modifier restricts access the most for what we need?
   b. If it is a field, could we restrict the access to ``private`` and use
      getters and setters?
   c. If we do set fields to ``private``, what access level do we have to give
      our getters and setters?
