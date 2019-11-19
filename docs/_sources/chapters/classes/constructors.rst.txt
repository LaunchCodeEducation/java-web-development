Constructors
============

We’ll often want to initialize, or set the initial value of, some of our
fields when creating a new object from a class. **Constructors** allow us to do
so.

In Java, constructors have the same name as the class and are most often
declared public (though they can have any other valid access modifier).
They are declared *without a return type*. Any function that is named
the same as the class and has no return type is a constructor.

Here is an example of a constructor definition within the ``HelloWorld``
class:

.. sourcecode:: java
   :linenos:

   public class HelloWorld {

       private String message = "Hello World";

       public HelloWorld(String message) {
           this.message = message;
       }

       public String getMessage() {
           return message;
       }

       public void setMessage(String aMessage) {
           message = aMessage;
       }

   }

This constructor allows us to create ``HelloWorld`` objects with custom
messages. The assignment ``this.message = message`` assigns the value
passed into the constructor to the field ``message``. Here’s how we
might use it:

.. sourcecode:: java

   HelloWorld goodbye = new HelloWorld("Goodbye World");
   System.out.println(goodbye.getMessage()); // prints "Goodbye World"


.. index:: ! default constructor

It’s not required that every class have a constructor. If you don’t
provide one, the Java compiler will generate an empty constructor for
you, known as a **default constructor**. For example, when we left out a
constructor in our ``HelloWorld`` class above, the compiler created the
following constructor for us:

.. sourcecode:: java

   public HelloWorld() {}

While this can be convenient, you almost always want to provide a
constructor to properly initialize your objects.

Overloading Constructors
------------------------

We can provide multiple constructors for a given class in order to allow
for different initialization scenarios. This is known as **constructor
overloading**. When providing multiple constructors, we must ensure that
each has a different collection of arguments, as determined by the
number, order, and type of the constructor arguments.

Let’s expand upon our ``Student`` class.

.. admonition:: Example

   .. sourcecode:: java
      :linenos:

      public class Student {

         private String name;
         private final int studentId;
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
            this.name = name;
            this.studentId = studentId;
            this.numberOfCredits = 0;
            this.gpa = 0.0;
         }

         /* getters and setters omitted */

      }

The first constructor allows for the creation of ``Student`` objects
where the code creating the object provides initial values for each of
the fields. The second allows for the creation of ``Student`` objects
with only ``name`` and ``studentId``. The first constructor would be
most useful for creating a transfer student, where credits and a GPA
might already be non-zero. However, for all new students, it would be
safe to initialize ``numberOfCredits`` and ``gpa`` to be 0.

A better way to write the above constructors would be this:

.. admonition:: Example

   .. sourcecode:: java
      :linenos:

      public class Student {

         private String name;
         private final int studentId;
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

         /* getters and setters omitted */

      }

In the example above on line 17, we use ``this()`` to invoke another
constructor within the same class. In this case, the second constructor calls
the first with the default values for ``numberOfCredits`` and ``gpa``. If you
use this syntax, the call to ``this()`` must be the first line in the
constructor. This is a good practice not only because it makes your code
shorter, but also because it allows any initialization behavior that may
be carried out beyond just initializing variables to be contained in a
smaller number of constructors. In other words, constructors can share
initialization code. Notice from this example that a constructor doesn’t
need to require an initial value for each field as an argument.

When defining constructors, think about:

#. Which fields must be initialized for your class to work properly? Be sure
   you initialize every such field.
#. Which fields should be initialized by the user creating an object, and
   which should be initialized by the class itself?
#. What are the use-cases for your class that you should provide for?

Check Your Understanding
------------------------

.. admonition:: Question

   A constructor is required for every class.

   A. True
   B. False

.. ans: False, a constructor is not required for every class.

.. admonition:: Question

   Let's take a look at a class called ``Dog``.

   .. sourcecode:: java
      :linenos:

      public class Dog {
         private String name;
         private String breed;

         public Dog(String name, String breed) {
            this.name = name;
            this.breed = breed;
         }
      }

   What line of code would be appropriate for us to declare an instance of the ``Dog`` class called ``myDog`` and give it the name, "Bernie", and the breed, "Beagle"?

   A. ``Dog myDog = new Dog(Bernie,beagle);``
   B. ``Dog myDog = new Dog("Bernie","beagle");``
   C. ``Dog Bernie = new Dog("Bernie","beagle");``

.. ans: The correct answer is B.
