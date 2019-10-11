Encapsulation
=============

Our discussion of classes and objects is integral to us using **object-oriented programming**.
Object-oriented programming stands on four pillars: abstraction, encapsulation, inheritance, and polymorphism.

.. index:: ! encapsulation

Encapsulation
-------------

**Encapsulation** is the bundling of related data and behaviors that operate on that data, usually with restricted access to internal, non-public data and behaviors.
In object-oriented programming, classes and objects allow us to encapsulate, or isolate, data and behavior to only the parts of our program to which they are relevant.
Restricting access allows us to expose only that data and behavior that we want others to be able to use.

Let's take a look at this by developing a new class called ``Student``.

``Student`` Class
-----------------

Fields
^^^^^^

We previously defined a **field** as a variable, or piece of data, that
belongs to a class. For our ``Student`` class, let’s think about the
data that is typically associated with a student (in the sense of a high
school or college student). There are a lot of possibilities, but here
are the most important:

1. Name
2. Student ID
3. Number of credits
4. GPA

In order to declare these fields within our class, we’ll need to
determine the best data type for each. A field may be of any primitive
or object type. In this case, the following types will work best:

1. Name: ``String``
2. Student ID: ``int``
3. Number of credits: ``int``
4. GPA: ``double``

Let’s put these inside of a class. While they may be declared anywhere
within a class, fields should always be declared at the top of the
class. When we’re ready to add methods, we’ll add them below the fields.

.. sourcecode:: java
   :linenos:

   public class Student {

       String name;
       int studentId;
       int numberOfCredits;
       double gpa;

   }

Like variables within a method, fields may be initialized when they are
declared. For example, we could provide default values for
``numberOfCredits`` and ``gpa`` (default values for ``name`` and
``studentId`` don’t make sense since they should be different for each
student).

.. sourcecode:: java

   int numberOfCredits = 0;
   double gpa = 0.0;

Fields are also referred to as **instance variables**, since they belong
to an instance of a class.

Getters and Setters
^^^^^^^^^^^^^^^^^^^

As declared, our four fields are package-private, which means that they
can be read or changed by any code within the same package. As a
rule-of-thumb, *fields should always be private unless you have a very,
very, very good reason to not make them so.* So, let’s make our
fields private.

.. sourcecode:: java
   :linenos:

   public class Student {

       private String name;
       private int studentId;
       private int numberOfCredits = 0;
       private double gpa = 0.0;

   }

In order to provide access to private fields, **getter and setter
methods** are used. Getters and setters do what you might guess: get and
set a given field. If we make the getter and/or setter method for a
given property public, then others will be able to access or modify the
field in that way.

Here is a getter/setter pair for ``name`` (you can imagine how the
others would be written).

.. sourcecode:: java
   :linenos:

   public String getName() {
       return name;
   }

   public void setName(String aName) {
       name = aName;
   }

.. note::

   Prefixing a parameter that is intended to set an instance variable with
   ``a`` is a relatively common convention, and one that we’ll adopt to
   avoid shadowing and having to use ``this`` in our setters. You can think
   of the ``a`` as denoting the “argument” version of the variable.

An astute question to ask at this point would be, “Why make the fields
private if you’re just going to allow people to get and set them
anyway!?” Great question. There are lots of reasons to use getters and
setters to control access. Here are just a few:

1. Sometimes you’ll want to implement behavior that happens every time a
   field is accessed (get) or changed (set). Even if you can’t think of
   such a reason when writing your class, you might later have the need
   to add such behavior. If you don’t use getters and setters, you’ll
   have to do a lot more refactoring if you ever decide to add such
   behaviors.
2. You can perform validation within a setter. For example, we might
   want to ensure that a student’s name contains only certain
   characters, or that their student ID is positive.
3. You can use different access modifiers on getters and setters for the
   same field, based on desired usage. For example, you might want to
   allow anyone to be able to read the value of a field, but only
   classes within the same package to modify it. You could do this with
   a public getter and a package-private setter, but not as a field
   without getters and setters, which could only be public to everyone
   or package-private to everyone.

As an example of reason 2, let’s take a short detour to look at a
``Temperature`` class. A valid temperature can only be so low (“absolute
zero”), so we wouldn’t want to allow somebody to set an invalid value.
In ``setFahrenheit`` we print out if an invalid value is
provided.

.. sourcecode:: java
   :linenos:

   public class Temperature {

       private double fahrenheit;

       public double getFahrenheit() {
           return fahrenheit;
       }

       public void setFahrenheit(double aFahrenheit) {

           double absoluteZeroFahrenheit = -459.67;

           if (aFahrenheit < absoluteZeroFahrenheit) {
               System.out.println("Value is below absolute zero");
           }

           fahrenheit = aFahrenheit;
       }
   }

.. note::

   When writing getters and setters, the convention for a field named
   ``field`` is to name them ``getField`` and ``setField``. This is more
   than just a convention, as some libraries you use will *expect* names to
   be of this format, and won’t work as desired if you don’t follow the
   convention.

   Additionally, it’s a standard convention to use ``is`` instead of
   ``get`` for boolean fields. So a boolean field ``oldEnoughToVote`` would
   have the “getter” method ``isOldEnoughToVote``. The setter should still
   be named ``setOldEnoughToVote``.

Properties
^^^^^^^^^^

A **property** in Java is a characteristic that users can set. Our
``Student`` class had properties ``name``, ``studentId``,
``numberOfCredits``, and ``gpa``, while our ``Temperature`` class had
only one property, ``fahrenheit``.

Most often, properties will be fields that have public setters, though
they need not have a corresponding field. Let’s look at an example of a
property that doesn’t directly correspond to a field. If we wanted to
add a ``celsius`` property to the ``Temperature`` class above, we might
do it as follows:

.. sourcecode:: java
   :linenos:

   public double getCelsius() {
       return (fahrenheit - 32) * 5.0 / 9.0;
   }

   public void setCelsius(double celsius) {
       double fahrenheit = celsius * 9.0 / 5.0 + 32;
       setFahrenheit(fahrenheit);
   }

Since there’s a link between ``fahrenheit`` and ``celsius``, we want to make
sure that when one is updated, so is the other. In this case, we only
store one field value (``fahrenheit``) and make the appropriate
calculation when getting or setting the ``celsius`` property.

.. note::

   There are slight variations among Java developers when it comes to
   colloquial usage of the term *property*. People will sometimes define
   the term in a slightly more specific or narrow way, to mean a private
   field with public getters and setters.

   Our definition here relies on the more general definition given by
   Oracle.

Using properties, getters/setters, and fields, we can *encapsulate* the information we need in our student class.

Check Your Understanding
------------------------

.. admonition:: Question

   What is a method that is used to give a private field a value?

   a. getter
   b. method
   c. property
   d. setter

.. ans: A setter is a method that gives a private field a value.