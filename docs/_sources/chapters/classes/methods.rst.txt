Methods
=======

Calling Methods on Objects
--------------------------

.. index:: method

A **method** is a function that belongs to a class. In Java, all procedures
must be part of a class. Let’s revisit our ``HelloWorld`` class.

.. sourcecode:: java
   :linenos:

   public class HelloWorld {

       private String message = "Hello World";

       void sayHello() {
           System.out.println(message);
       }

   }

There is one method in this class, ``sayHello()``. In order to call this
method, we must have an object created from the ``HelloWorld`` class
template. In other words, we must have an instance of ``HelloWorld``.

Here’s how you call methods on an object.

.. sourcecode:: java

   HelloWorld hello = new HelloWorld();
   hello.sayHello();

It is not possible to call ``sayHello()`` without having a ``HelloWorld``
object. This begins to make more sense when you note that the
``message`` field is used within ``sayHello()``, and unless we are calling
``sayHello()`` on an instantiated object, there will be no ``message``
field available to print.

.. note::

   As mentioned before, class members should have the most restrictive
   level of access possible. This goes for methods as well as fields. For
   example, if you create a utility method that should only be used within
   your class, then it should be ``private``. You can think of ``private``
   methods as those that are not useful *outside* of the class, but that
   can contribute internally to helping the class behave as desired or
   expected.

   On the contrary, ``public`` methods are code that other classes will
   want to use when they implement the class containing those ``public``
   methods. So only make methods ``public`` when you expect other classes
   to use them, and when you are committed to maintaining those methods for
   other calling programs that may use them.

.. index:: ! instance method

Instance Methods
----------------

So far, we’ve only looked at examples of methods that are relatively
specialized: constructors, getters, and setters. Every class you create
will have these methods. What will make your classes different from each
other, and thus fulfill the purpose of creating each class, are the
specific behaviors that are unique to your classes.

Let’s say we want to add a method in our ``Student`` class that reports the GPA
of a student. This method is an **instance method** since it will belong to
each ``Student`` object created, and will use the data of each such object.

.. sourcecode:: java
   :linenos:

   public class Student {

       private static int nextStudentId = 1;
       private String name;
       private int studentId;
       private int numberOfCredits;
       private double gpa;

       public Student(String name, int studentId, int numberOfCredits, double gpa) {
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

       /* getters and setters omitted */

   }

We will make use of instance methods more in the next chapter, however, we
wanted to share more about them now in our first conversation about classes.
Sometimes when we create a class, we will need that class to have more
behaviors than using only constructors, setters, and getters can provide. When
we do want to add additional behaviors to our classes, we can use instance
methods!

Check Your Understanding
------------------------

.. admonition:: Question

   Fill in the blanks with the appropriate terms.

   A _____________ gives a class property a field.
   A _____________ gives a programmer access to the value of a private class property.
   A _____________ creates a new instance of a class with values for the fields.
   A _____________ is a method that belongs to each instance of a class.

.. ans: setter, getter, constructor, instance
