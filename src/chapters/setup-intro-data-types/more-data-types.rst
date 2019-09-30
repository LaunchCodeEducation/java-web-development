More Data Types
================

Class Types
------------

.. index:: ! class

Java classes and objects are conceptually the same as in JavaScript. A
**class** is a template for creating objects. In addition to the data types
introduced so far, any class in Java also defines a type. We’ll have much more
to say about classes and objects, but for now you need to recognize the basic
syntax of class types and class creation.

In JavaScript, if we have a class ``Cat`` with a constructor that takes no
arguments, we can declare and create an instance of ``Cat`` using the ``new``
keyword:

.. sourcecode:: JavaScript

   let myCat = new Cat();

In Java, the syntax is:

.. sourcecode:: java

   Cat myCat = new Cat();

Each of these statements declares and initializes a variable with a new ``Cat``
object. The difference in Java is that we must declare the variable’s type.

.. index:: ! reference type

Just like variables or parameters can be declared as an ``int`` or ``String``
data type, they can also be declared as a specific *class* type. Variables
that are class type---as opposed to primitive types like ``double`` or object
types like ``String``---are said to be of **reference type**. Using this
terminology, ``myCat`` is a *reference variable* of type ``Cat``.

References
^^^^^^^^^^^

Reference types are different from primitive types in an essential way. A
variable of a reference type (such as ``myCat`` above) does not actually store
the object in question. Instead, it stores a **reference** to the object. A
reference is literally a memory address. We visualize references as an arrow
pointing to the object in memory.

Consider this code:

.. sourcecode:: java
   :linenos:

   int firstCatAge = 11;
   int secondCatAge = firstCatAge;
   Cat myCat = new Cat();
   Cat sameCat = myCat;

Visually, we can represent these four variables as shown below.

.. figure:: figures/references.png
   :alt: Reference Types

   Reference Types vs. Primitive Types

Since ``int`` is a primitive type, the variables ``firstCatAge`` and
``secondCatAge`` function like separate boxes, each one holding the integer
value ``11``. On the other hand, ``myCat`` is a reference variable, since it
holds an object of type ``Cat``. The variable actually stores the *memory
address* of the object, which we visualize as an arrow from the variable box to
where the data is stored. Instead of holding the actual ``Cat`` data, ``myCat``
stores *directions* for finding the data in memory.

When we assign a value to a reference type, as in ``Cat sameCat = myCat``, we
are not creating a second copy of the object or its data. Instead, we create a
second arrow pointing to the same memory location.

The distinction between reference types and primitives is important, if
subtle. As you continue learning Java, you will see that reference types are
handled differently in essential and important ways.

Arrays
-------

In unit 1, we frequently used arrays in JavaScript to store ordered collections
of data---strings, numbers, objects, other arrays, etc. In your exercises,
studios, and assignments, you often mutated arrays by rearranging the elements
or by adding/removing data.

.. sourcecode:: JavaScript
   :linenos:

   let firstArray = [1, 2, 3];
   let secondArray = ['LC101', 42, ['Hello', 'World'], {name: "Fabulous Fox", astronautID: 12, age: 5}];

   firstArray.reverse().push('LaunchCode ROCKS!');
   // Results in [3, 2, 1, 'LaunchCode ROCKS!']

In Java, an array is an ordered, *fixed-size* collection of elements. Since
Java is statically-typed, the items stored in an array must all be the same
data type. We can create an array of integers or an array of strings, but we
may NOT create an array that holds both integers and strings.

The syntax for creating an array capable of holding 10 integers is:

.. sourcecode:: java

   int[] someInts = new int[10];

To create an array of a different size, replace the number ``10`` in the
brackets with the desired size. To create an array holding a different type,
replace ``int`` (on both sides of the assignment) with the desired type, like
``double``.

In addition to the example above, we can initialize an array using a literal
expression:

.. sourcecode:: java

   int[] someOtherInts = {1, 1, 2, 3, 5, 8};

Here, the size is implicit in the number of elements in the literal
expression ``{1, 1, 2, 3, 5, 8}``. Also note the use of braces ``{ }`` instead
of square brackets ``[ ]``.

To access array elements, we use square brackets and *zero-based indexing* just
like in JavaScript.

.. sourcecode:: java

   int anInt = someOtherInts[4];
   // anInt stores the integer 5.

Unlike in JavaScript, arrays in Java may NOT change size once created, which is
not very practical. Thankfully, Java provides more flexible ways to store data,
which we will explore in a later lesson.

Aside from using arrays to build some simple loop examples, we will only use
them in special cases. However, they are a core part of Java, so it’s good to
know how they work, especially since the term "arrays" in JavaScript refers to
something with much different behavior.

.. _static-methods:

Static Methods
---------------

In pure object-oriented languages like Java and C#, we don’t have functions in
the sense you’re used to. Unlike JavaScript, functions may NOT be declared
outside of a class. Even a simple function that checks if an integer is even
needs to be defined within a class.

.. index:: ! methods

Within the context of a class, functions are referred to as **methods**, and we
will adopt this terminology from now on.

.. admonition:: Warning

   Be prepared for push-back and negative judgement from Java coders if you
   accidentally refer to methods as “functions”.

.. index:: ! static methods

We’ll dive deeper into classes and objects in Java soon enough. For now, we
will explore how to write methods. In particular, we’ll use **static methods**,
which behave similarly to the functions you built in JavaScript.

A static method is one that can be called without creating an instance of the
class to which it belongs.

.. admonition:: Example

   Define the class ``Cat`` and include the ``static`` keyword before the
   ``makeNoise`` method name:

   .. sourcecode:: java

      public class Cat {
         public static void makeNoise(String[] args) {
            // some code
         }
      }

   Since ``makeNoise`` is ``static``, we do NOT need to create a ``Cat`` object to
   access it.

   Instead of doing this:

   .. sourcecode:: java
      :linenos:

      Cat myCat = new Cat();     // Create a new Cat object.
      myCat.makeNoise("purr");   // Call the makeNoise method.

   We can call the method directly:

   .. sourcecode:: java
      :linenos:

      Cat.makeNoise("roar");

Until we get further into Object Oriented Programming, every method you write
should use the ``static`` keyword. Leaving off ``static`` will prevent or
complicate the process of calling the methods you defined.

We will explore exactly what ``static`` does in more detail in later lessons.

Static Method Practice
^^^^^^^^^^^^^^^^^^^^^^^

Let’s create two classes in Java to practice defining and using methods. The
first class will have a ``main`` method and the second will have a method that
we want to call from within ``main``.

.. admonition:: Examples

   HelloMethods.java:

   .. sourcecode:: java
      :linenos:

      public class HelloMethods {

         public static void main(String[] args) {
            String message = Message.getMessage("fr");
            System.out.println(message);
         }

      }

   Message.java:

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

We won’t explore every new aspect of this example, but instead focus on the two
methods.

#. The ``main`` method in the ``HelloMethods`` class is the same in
   structure as that of our
   :ref:`temperature conversion example <temp-conversion>`.
#. Take a look at the ``Message`` class. Note that it does NOT have a ``main``
   method, so it can’t be run on it’s own. Code within the ``Message`` class
   must be called from elsewhere in order to execute.
#. The ``Message`` class contains the ``getMessage`` method. Like ``main``, it
   has the ``static`` keyword. Unlike ``main``, ``getMessage`` has a return
   type of ``String``. It also has a single ``String`` parameter, ``lang``.

Since Java is statically typed, creating methods will be similar to writing
`functions in TypeScript <https://education.launchcode.org/intro-to-professional-web-dev/chapters/typescript/functions.html#functions-in-typescript>`__.
We must declare the data type for each parameter, AND we must declare the data
type for the return value.

.. sourcecode:: java

   public static returnedDataType methodName(parameterDataType parameterName) {
      //code
   }

One consequence of this is that a method in Java may NOT have ``return``
statements that send back different types of data. Note that lines 6, 8, and 10
in ``Message.java`` each return a string. If we try to replace line 10 with
``return 42;``, then we would generate a compiler error.

To call a static method, we follow a specific syntax. Line 4 in the
``HelloMethods.java`` shows this:

.. sourcecode:: java

   Message.getMessage("fr");

To call a static method we must use the format
``ClassName.methodName(arguments)``.

Note that ``getMessage`` is NOT defined within the ``HelloMessage`` class. We
can do this because ``getMessage`` is declared as ``public``. If we wanted to
restrict the method from being called by another class, we could instead use
the ``private`` modifier. We will explore access modifiers in more depth in
coming lessons.

   TODO: Ask about the implications of a repository with the code samples
   mentioned in this section.

.. admonition:: Warning

   As you’ve been following along with these examples using the code in
   IntelliJ, you’ve probably noticed that each class file, for example
   ``Message.java`` and ``HelloMethods.java``, is named exactly the same as
   the class it holds (``Message`` and ``HelloMethods``, respectively).

   It is a rule in Java that a file containing a class marked ``public``
   MUST be named the same as that class.

References
----------

#. `Arrays (docs.oracle.com) <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html>`__

Check Your Understanding
-------------------------

Lorem ipsum...
