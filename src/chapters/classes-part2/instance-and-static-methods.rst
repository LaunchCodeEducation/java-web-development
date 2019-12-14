Instance and Static Methods
============================

We explored configuring *data* within classes with fields and properties. Now
let’s turn our attention back to class *behavior* (methods).

Quick Method Review
--------------------

In the :ref:`last chapter <classes-part1>`, we learned that:

#. A *method* belongs to a class and performs an action.
#. Methods cannot stand on their own---they must be part of a class.
#. To call a method on an object, use dot notation:

   .. sourcecode:: java

      objectName.methodName(arguments);

#. Access modifiers apply to methods:

   a. ``private`` methods as those that are NOT useful outside of the class but
      contribute internally to helping the class behave as desired or expected.
   b. ``public`` methods contain code that other classes need to use when they
      implement the class containing those methods. Make methods ``public``
      only when you expect other classes to use them, and when you are
      committed to maintaining those methods for other programs.

Let's take a closer look at two different types of methods---both of which we
have used in earlier examples.

.. index:: instance method

.. _instance-methods:

Instance Methods
----------------

As we learned in the last chapter, *instance methods* define the behaviors that
are *unique* or *specialized* to each class. Every object created from a class
will carry a copy of these methods.

Instance methods depend on the data stored in an individual object. If two
objects call the same method, the results will vary when the objects contain
different data.

Let’s add a couple more instance methods to our ``Student`` class.

What are the behaviors that our ``Student`` class should have? To start, it
makes sense that when a student takes a class and earns a grade, their data
should be updated accordingly. Additionally, it would be nice to easily
identify the grade level of a student---freshman, sophomore, junior, or senior.

The framework for these new methods is shown in the ``Student`` class below,
but each method is missing some code. Filling in that code is left for you to
do in the chapter exercises.

.. sourcecode:: java
   :linenos:

   public class Student {

      private static int nextStudentId = 1;
      private String name;
      private int studentId;
      private int numberOfCredits;
      private double gpa;

      public Student(String name, int studentId,
            int numberOfCredits, double gpa) {
         this.name = name;
         this.studentId = studentId;
         this.numberOfCredits = numberOfCredits;
         this.gpa = gpa;
      }

      public Student(String name, int studentId) {
         this(name, studentId, 0, 0);
      }

      public Student(String name) {
         this(name, nextStudentId);
         nextStudentId++;
      }

      public String studentInfo() {
         return (this.name + " has a GPA of: " + this.gpa);
      }

      public void addGrade(int courseCredits, double grade) {
         // Update the appropriate fields: numberOfCredits, gpa
      }

      public String getGradeLevel() {
         // Determine the grade level of the student based on numberOfCredits
      }

      /* getters and setters omitted */

   }

.. admonition:: Tip

   When creating your classes, think about the behaviors that you want to
   make available, as well as the access level of those methods.

Static Methods
--------------

We’ve already used static methods quite a bit in this course, all the way back
to our first Java method:

.. sourcecode:: java

   public static void main(String[] args) {}

Now let’s examine them in the context of what we’ve recently learned about
classes.

.. index:: static methods, ! class methods

Just like static fields, **static methods** belong to the class as a whole, and
not to any of the specific instances of the class. Thus, they are sometimes
also called **class methods**. A static method is essentially the opposite of
an instance method, since the two cases are mutually exclusive.
*Instance methods* rely on each object’s specific data, while *static methods*
must NOT rely on data from a specific object.

We call a static method by preceding it with the class name and using
dot-notation. Here’s an example that we looked at
:ref:`previously <more-data-types-static-method-example>`.

.. admonition:: Examples

   ``HelloMethods.java``

   .. sourcecode:: java
      :linenos:

      public class HelloMethods {

         public static void main(String[] args) {
            String message = Message.getMessage("fr");
            System.out.println(message);
         }

      }

   ``Message.java``

   .. sourcecode:: java
      :linenos:

      public class Message {

         public static String getMessage(String lang) {

            if (lang.equals("sp")) {
                  return "¡Hola, Mundo!";
            } else if (lang.equals("fr")) {
                  return "Bonjour, le monde!";
            } else {
                  return "Hello, World!";
            }
         }
      }

The call occurs in line 4: ``Message.getMessage("fr")``. We call the static
``getMessage`` without needing an instance of the ``Message`` class. Instead,
we use the name of the class itself.

.. admonition:: Warning

   It is technically allowed to call a static method using an instance of a
   class: ``myObject.someStaticMethod()``. However, best practice recommends
   using the class name instead: ``ClassName.someStaticMethod()``. This makes
   it clear to other coders that you are calling a static method.

A method should be static when it does NOT refer to any instance fields of the
containing class (it *may* refer to static fields, however). These methods tend
to be utility-like (e.g. carrying out a calculation, or using or fetching some
external resource).

Accessing Static vs. Instance Fields
-------------------------------------

One common error new Java coders encounter reads something like *non-static
variable cannot be referenced from a static context*. This occurs when a
*static method* tries to call an *instance variable*.

Why can't we do this? Static methods can be called from anywhere (depending on
their access modifier), and they do NOT require us to create an object for a
particular class. However, these methods must be independent of any values
unique to a particular object.

For example, if we have a ``Circle`` class, then we can define and call a
static ``area`` method without creating a new object:
``Circle.area(radius)``. Since the area of a circle is just,
``PI*radius*radius``, we can pass in the argument when we call the method. The
method does not depend on any value stored within a specific ``Circle`` object.

Now let's assume we define a ``Car`` class with an instance variable for
``color``. The value of this field will NOT be the same for every ``Car``
object we create. Thus, trying to call a static method like
``Car.printColor()`` results in an error. Since there is no single value for
``color`` that applies to every object, trying to access it from outside of the
class does not work. To print the color of a ``Car`` object, we must call the
method on that specific object: ``myCar.printColor()``.

Instance fields can only be called by instance methods.

.. admonition:: Note

   While static methods cannot access instance variables, an instance method
   CAN access a static variable. Why?

References
-----------

#. `Encapsulation
   (wikipedia.org) <https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)>`__
#. `Defining Methods
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/javaOO/methods.html>`__
#. `Passing Data to a Method or Constructor
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/javaOO/arguments.html>`__

Check Your Understanding
-------------------------

.. admonition:: Question

   Assume that we add two methods to a ``Pet`` class---``public String makeNoise()``
   and ``public static void increaseAge()``. Which of the following statements is
   true?

   #. The ``makeNoise()`` method can be accessed outside of the ``Pet`` class,
      while the ``increaseAge()`` method cannot.
   #. Each ``Pet`` object carries a copy of the ``makeNoise()`` method but NOT
      a copy of the ``increaseAge()`` method.
   #. The ``increaseAge()`` method can be accessed outside of the ``Pet`` class,
      while the ``makeNoise()`` method cannot.
   #. Each ``Pet`` object carries a copy of the ``increaseAge()`` method but
      NOT a copy of the ``makeNoise()`` method.

.. The correct answer is "b".

.. admonition:: Question

   Explain why it IS possible for an instance method to access a static field.

.. There is no problem with this because static variables belong to a class and
   can be called from anywhere (depending on the access modifier). Thus, any
   instance method can access them from outside of the class where they are
   defined.
