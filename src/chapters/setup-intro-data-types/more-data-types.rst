More Data Types
================

Class Types
-----------

In addition to the types introduced so far - primitives and their
objectified counterparts - any class in Java defines a type. Classes and
objects are conceptually the same as in Python: A class is a template
for creating objects. We’ll have much more to say about classes and
objects, but for now you need to be comfortable seeing the basic syntax
of class types and class creation.

If I have a class ``Cat`` with a constructor that takes no arguments, I
can declare and create a new instance of ``Cat`` using its constructor.
In Python, we did this as follows:

.. code:: python

   # Python
   my_cat = Cat()

And the Java version is:

.. code:: java

   Cat myCat = new Cat();

Each of these statements creates a new variable that is initialized to
hold a new ``Cat`` object. Note that in Java, we must declare the
variable’s type. Also note that we precede the constructor with the
``new`` keyword. And, of course, the Java example ends with a
semi-colon.

Variables and parameters that are of the type of a class are said to be
of **reference type** (in contrast to **primitive type**). In plain
English, we would say of the Java example: “``myCat`` is a reference
variable of type ``Cat``.”

References
^^^^^^^^^^^

Reference types are different from primitive types in an essential way.
A variable of a reference type (such as ``myCat`` above) does not
actually store the object in question. Instead, it stores a
**reference** to the object. A reference is literally a memory address.
We visualize references as an arrow pointing to the object in memory.

Consider this code:

.. code:: java

   int catAge = 11;
   Cat myCat = new Cat();
   Cat sameCat = myCat;

Visually, we can represent these three variables as shown below.

.. figure:: figures/references.png
   :alt: Reference Types

   Reference Types

Since ``int`` is a primitive type, the variable ``catAge`` functions as
a box holding the integer value 11. On the other hand, ``myCat`` is a
reference variable, since it holds an object. The variable actually
stores the address of the object, which we visualize as an arrow from
the variable box to the object.

When we assign a value to a reference type, as in
``Cat sameCat = myCat``, we are not creating a second copy of the
object, but instead are creating a second “arrow” pointing to the same
object.

The distinction between references types and primitives is important, if
difficult, to wrap your brain around at first. We will see that
reference types are handled differently in essential and important ways
in a lot of different situations.

Arrays
------

Just as Java has primitive types for things that were objects in Python
– such as integers and booleans – it also has a type that you might
consider to be a “primitive list”, arrays.

An array is an ordered, fixed-size collection of elements. Since Java is
statically-typed, arrays may only store one type of object. We can
create an array of integers or an array of strings, but we may not
create an array that holds both integers and strings.

The syntax for creating an array capable of holding 10 integers is:

.. code:: java

   int[] someInts = new int[10];

To create an array of a different size, replace the number 10 in
brackets with the desired size. To create an array holding a different
type, replace ``int`` (on both sides of the assignment) with the desired
type, for instance, ``double``. Unlike lists in Python, arrays in Java
*may not* change size once created. This turns out to be not very
practical, so thankfully Java provides more flexible ways to store data,
which we’ll explore in a later lesson.

In addition to the technique above, we can initialize an array using a
literal expression:

.. code:: java

   int[] someOtherInts = {1, 1, 2, 3, 5, 8};

Here, the size is implicit in the number of elements in the literal
expression ``{1, 1, 2, 3, 5, 8}``.

To access array elements, we use square brackets, as with Python lists.

.. code:: java

   int anInt = someInts[0];

As with Python lists, arrays have *zero-based indexing*.

Aside from using arrays to build some simple loop examples in the next
lesson, we’ll only use them in special cases. However, they’re a core
part of Java, so it’s good to know how they work.

.. _static-methods:

Static Methods
--------------

In pure object-oriented languages like Java and C#, we don’t have
functions in the sense you’re used to. For example, functions may not be
declared outside of a class. Within the context of a class, functions
are referred to as **methods**. We will adopt this terminology from now
on, and you are encouraged not to refer to methods as “functions” when
you are talking about Java code.

We’ll dive into learning about classes and objects in Java soon enough,
but until we do, we’ll frequently need to write methods, so we should
understand a little bit about them. In particular, we’ll use **static
methods**, which behave similarly to functions as you knew them in
Python.

A static method is one with the ``static`` keyword, as our ``main``
method above has:

.. code:: java

   public static void main(String[] args)
   {
       // some code
   }

We’ve already explored each element of this line, however, we haven’t
really shown you how you might create your own methods in other
contexts. To do so involves using a different name for our method, and
adjusting the return type and parameter types accordingly.

.. raw:: html

   <aside class="aside-warning">

Until we get into Object Oriented Programming, every method we write
will have the ``static`` keyword. Leaving off ``static`` will prevent
you from calling methods you define as you would like to.

We will explore exactly what ``static`` does in more detail in later
lessons.

.. raw:: html

   </aside>

Let’s create two classes in Java to demonstrate this. One will have a
``main`` method and the other will have a method that we want to call
from within ``main``.

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

We won’t explore every new aspect of this example, but rather will focus
on the two methods.

.. raw:: html

   <aside class="aside-warning">

As you’ve been following along with these examples using the code in
IntelliJ, you’ve probably noticed that each class file, for example
``Message.java`` and ``HelloMethods.java``, is named exactly the same as
the class that file holds, for example ``Message`` and ``HelloMethods``
respectively.

It is a rule in Java that a file containing a class marked ``public``
**must** be named the same as that class. So remember to name each Java
file you create to match the public class that file contains.

.. raw:: html

   </aside>

The ``main`` method in the ``HelloMethods`` class is the same in
structure as that of our previous examples. Take a look at the
``Message`` class. Note that it *does not* have a ``main`` method, so it
can’t be run on it’s own. Code within the ``Message`` class must be
called from elsewhere in order to execute.

The ``Message`` class has a method of its own: ``getMessage``. Like
``main``, it has the ``static`` keyword. Unlike ``main``, ``getMessage``
has a return type of ``String``. It also has a single parameter,
``String lang``.

Since Java is statically typed, each method must declare its return type
– that is, the data type of what it will return – along with the type of
each parameter. One consequence of this that may not be immediately
obvious is that a method in Java may not have return statements that
return different types of data. For example, we would not be able to
replace the last ``return`` statement of ``getMessage`` with something
like ``return 42;``. This would be flagged as a compiler error.

Finally, let’s note how a static method is called. The first line of
``main`` in the ``HelloMethods`` class is:

.. code:: java

   Message.getMessage("fr");

To call a static method we must use the name of the class in which it is
defined, followed by ``.``, followed by the name of the method.

We are able to call this method from another class because it is
declared to be ``public``. If we wanted to restrict the method from
being called by another class, we could instead use the ``private``
modifier. We’ll explore access modifiers in more depth in coming
lessons.