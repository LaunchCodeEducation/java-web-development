Methods
=======

Calling Methods on Objects
--------------------------

A **method** is a procedure that belongs to a class. In Java, all
procedures must be part of a class. Let’s revisit our ``HelloWorld`` class.

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

Instance Methods
----------------

So far we’ve only looked at examples of methods that are relatively
specialized: constructors, getters, and setters. Every class you create
will have these methods. What will make your classes different from each
other, and thus fulfill the purpose of creating each class, are the
specific behaviors that are unique to your classes.

Let’s add a couple of such methods to our ``Student`` class. These
methods will be **instance methods** since they will belong to each
``Student`` object created, and will use the data of each such object.

What are the behaviors that our ``Student`` class should have? To start,
it would make sense for a student to take a class and get a grade, and
for their data to be updated accordingly. Additionally, it would be nice
to be able to easily tell the grade level of a student – freshman,
sophomore, junior, or senior.

Our last look at the ``Student`` class stubs out these methods below,
without providing the implementation. That job is left to you to do as
an exercise.

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

       public void addGrade(int courseCredits, double grade) {
           // Update the appropriate fields: numberOfCredits, gpa
       }

       public String getGradeLevel() {
           // Determine the grade level of the student based on numberOfCredits
       }

       /* getters and setters omitted */

   }

When creating your classes, think about the behaviors that you want to
make available, as well as the access level of those methods.

Check Your Understanding
------------------------

.. admonition:: Question

   What is are the differences between an instance method, a getter, a setter, and a constructor?