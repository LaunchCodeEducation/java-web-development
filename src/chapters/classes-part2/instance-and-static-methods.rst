Instance and Static Methods
============================

We explored configuring *data* within classes with fields and properties. Now
let’s turn our attention to *behavior* (methods).

.. index:: method

Calling Methods on Objects
--------------------------

A *method* is a procedure that belongs to a class. In Java, all procedures must
be part of a class---they cannot stand on their own. Let’s revisit our minimal
class example.

.. sourcecode:: java
   :linenos:

   public class HelloWorld {

      private String message = "Hello World";

      void sayHello() {
         System.out.println(message);
      }

   }

There is one method in this class, ``sayHello``. In order to call this method,
we must create an object from the ``HelloWorld`` class template. In other
words, we must have an instance of ``HelloWorld``.

Here’s how you call methods on an object.

.. sourcecode:: java
   :linenos:

   HelloWorld hello = new HelloWorld();
   hello.sayHello();

It is not possible to call ``sayHello`` without having a ``HelloWorld``
object. This begins to make more sense when you note that the
``message`` field is used within ``sayHello``, and unless we are calling
``sayHello`` on an instantiated object, there will be no ``message``
field available to print.

.. admonition:: Tip

   As mentioned before, class members should have the most restrictive level
   of access possible. This goes for methods as well as fields.

   For example, if you create a method that should *only* be used within
   your class, then you should declare it ``private``. Think of ``private``
   methods as those that are NOT useful outside of the class but contribute
   internally to helping the class behave as desired or expected.

   ``public`` methods contain code that other classes need to use when they
   implement the class containing those methods. Make methods ``public`` only
   when you expect other classes to use them, and when you are committed to
   maintaining those methods for other programs that might need them.

.. index:: ! instance method

Instance Methods
----------------

So far we’ve only looked at examples of methods that are relatively
specialized: constructors, getters, and setters. Every class you create
will have these methods.

What makes your classes different from each other, and thus fulfills the
purpose of creating them, are the behaviors that are *unique* or
*specialized* to each class.

Let’s add a couple of such methods to our ``Student`` class. These methods will
be **instance methods**, since they belong to each ``Student`` object created,
and they use the data of each such object.

What are the behaviors that our ``Student`` class should have? To start, it
makes sense that when a student takes a class and earns a grade, their data
should be updated accordingly. Additionally, it would be nice to easily
identify the grade level of a student – freshman, sophomore, junior, or senior.

Our last look at the ``Student`` class stubs out these methods below,
without providing the implementation. That job is left to you to do as
an exercise.

.. code:: java

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

Static Methods
--------------

Static methods are not new to us. We’ve used them quite a bit, all the
way back to our first Java method:
``public static void main(String[] args)``. Now let’s present them in
the context of the rest of what we’ve recently learned about classes.

Analogous to static fields, **static methods** belong to the class as a
whole, and not to any of the specific instances of the class. Thus, they
are sometimes also called **class methods**. A static method can be
thought of as the opposite of an instance method, since the two cases
are mutually exclusive. Instance methods rely on each object’s specific
data whereas static methods must *not* rely on data from a specific
object.

A static method may be called by preceding it with the class name and
using dot-notation. Here’s an example that we looked at previously.

.. code:: java

   public class HelloMethods {

       public static void main(String[] args) {
           String message = Message.getMessage("fr");
           System.out.println(message);
       }

   }

.. code:: java

   public class Message {

       public static String getMessage(String lang) {

           if (lang.equals("sp")) {
               return "Hola Mundo";
           } else if (lang.equals("fr")) {
               return "Bonjour le monde";
           } else {
               return "Hello World";
           }
       }
   }

The call in question is: ``Message.getMessage("fr")``. We call the
static method ``getMessage`` without needing an instance of the
``Message`` class, using the name of the class itself.

.. raw:: html

   <aside class="aside-warning">

It is technically allowed to call a static method using an instance of a
class: ``myObject.someStaticMethod()``. However, this should be avoided
in favor of using the class name to call the method so that it is clear
you are using a static method.

.. raw:: html

   </aside>

A method should be static when it does not refer to any instance fields
of the containing class (it *may* refer to static fields, however).
These methods tend to be utility-like, carrying out a calculation, or
using or fetching some external resource.