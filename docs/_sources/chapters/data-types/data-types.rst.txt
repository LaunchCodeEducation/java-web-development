Data Types
===========

Static vs. Dynamic Typing
-------------------------

.. index:: ! dynamically typed, ! statically typed

In a **dynamically typed** programming language (like JavaScript or Python), a
variable or parameter can refer to a value of any data type (string, number,
object, etc.) at any time. When the variable is used, the interpreter figures
out what type it is and behaves accordingly.

Java is a **statically typed** language. When a variable or parameter is
declared in a statically typed language, the data type for the value must be
specified. Once the declaration is made, the variable or parameter cannot refer
to a value of any other type.

For example, this is legal in JavaScript, a dynamically typed language:

.. admonition:: Example

   .. sourcecode:: JavaScript
      :linenos:

      let dynamicVariable = "dog";
      console.log(typeof(dynamicVariable));
      dynamicVariable = 42;
      console.log(typeof(dynamicVariable));

   **Output**

   .. sourcecode:: bash

      string
      number

After line 1 executes, ``dynamicVariable`` holds a ``string`` data type. After
line 3 runs, ``dynamicVariable`` becomes a ``number`` type. ``dynamicVariable``
is allowed to hold values of different types, which can be reassigned as
needed when the program runs.

However, the corresponding code in Java will result in a compiler error:

.. admonition:: Example

   .. sourcecode:: java
      :linenos:

      String staticVariable = "dog";
      staticVariable = 42;

   **Output**

   .. sourcecode:: bash

      error: incompatible types: int cannot be converted to String

The compiler error occurs when we try to assign ``42`` to a variable of type
``String``.

Take-home lesson: *We must declare the type of every variable and parameter in
a statically typed language*. This is done by declaring the data type for the
variable or parameter BEFORE its name, as we did in the example above:
``String staticVariable = "dog"``.

.. admonition:: Note

   We only need to specify the type of a variable or parameter when declaring
   it. Further use of the variable or parameter does not require us to identify
   its type. Doing so will result in an error.

.. index:: ! type system

Dynamic and static typing are examples of different `type
systems <https://en.wikipedia.org/wiki/Type_system>`__. The **type system** of
a programming language is one of the most important high-level characteristics
that programmers use when discussing the differences between languages. Here
are a few examples of popular languages falling into these two categories:

#. **Dynamic**: Python, Ruby, Javascript, PHP
#. **Static**: Java, C, C++, C#, TypeScript

Because we need to give plenty of attention to types when writing Java code,
let’s begin by exploring the most common data types in this language.

Strings and Single Characters
------------------------------

Immutability
^^^^^^^^^^^^^

Strings in Java are *immutable*, which means that the characters within a
string cannot be changed.

Single vs. Double Quotation Marks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Java syntax requires double quotation marks when declaring strings.

Java has another variable type, ``char``, which is used for a single character.
``char`` uses single quotation marks. The single character can be a letter,
digit, punctuation, or whitespace like tab (``'\t'``).

.. sourcecode:: java
   :linenos:

   String staticVariable = "dog";
   char charVariable = 'd';

.. _string-methods:

Manipulation
^^^^^^^^^^^^

The table below summarizes some of the most common string methods available in
Java. For these examples, we use the string variable
``String str = "Rutabaga"``.

.. list-table:: String methods in Java
   :header-rows: 1

   * - Java Syntax
     - Description
   * - ``str.charAt(3)``
     - Returns the character at index 3, (``'a'``).
   * - ``str.substring(2,4)``
     - Returns the characters from indexes 2 - 4, (``"tab"``).
   * - ``str.length()``
     - Returns the length of the string.
   * - ``str.indexOf('a')``
     - Returns the index for the first occurrence of 'a', (``3``).
   * - ``str.split("delimiter")``
     - Splits the string into sections at each ``delimiter`` and stores the
       sections as elements in an array.
   * - ``str.concat(string2).concat(string3)``
     - In Java, ``concat`` concatenates only two strings. To join multiple
       strings, method chaining is required.
   * - ``str.trim()``
     - Removes any whitespace at the beginning or end of the string.
   * - ``str.toUpperCase(), str.toLowerCase()``
     - Changes all alphabetic characters in the string to UPPERCASE or
       lowercase, respectively.
   * - ``str.contains("text")``
     - Searches for the specified text within a string and returns ``true`` or
       ``false``.
   * - ``str.equals(otherString)``
     - Compares strings for equality and returns a boolean.

.. admonition:: Note

   We will explore the differences between using ``==`` and ``.equals()`` when
   we discuss Java operators. For now, use ``.equals()`` if you need to compare
   two strings.

Primitive Types
----------------

A primitive data type is a basic building block. Using primitive data types, we
can build more complex data structures called *object* data types.

Java uses its own a set of primitive data types. The table below shows the most
common types that beginners are likely to encounter. A more complete list can
be found on the
`Oracle website <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html>`__.

.. list-table:: Java Primitive Data Types
   :header-rows: 1

   * - Data Type
     - Examples
     - Notes
   * - ``int``
     - 42
     - Represents positive and negative whole numbers.
   * - ``float``
     - 3.141593 and 1234.567 and 2.0
     - Represents positive and negative decimal numbers with up to 7 digits.
   * - ``double``
     - 3.14159265358979 and 10000.12345678912
     - Represents positive and negative decimal numbers with 15-16 digits.
   * - ``char``
     - 'a' and '9' and '\n'
     - A single unicode character enclosed in single quotes ``''``.
   * - ``boolean``
     - ``true`` and ``false``
     - Booleans in Java are NOT capitalized.

.. admonition:: Warning

   As we will see in a later section, the ``float`` data type sacrifices some
   accuracy for speed of calculation. Thus, evaluating 1.11111 + 3 results in an
   answer of 4.1111097 instead of 4.11111.

   Anytime you need to perform calculations with decimal values, consider using
   the ``double`` type instead of ``float``.

Non-primitive Types
--------------------

Primitive data types are *immutable* and can be combined to build larger data
structures. One example is forming the ``String`` "LaunchCode" from multiple
``char`` characters ('L', 'a', 'u', etc.).

``String`` is a non-primitive data type, also called an *object type*. As we
saw in the ``String`` table above, object types have methods which we can call
using dot notation. Primitive data types do not have methods.

.. admonition:: Note

   Primitive data types in Java begin with a lower case letter, while object
   data types in Java begin with a capital letter.

Later in this chapter, we will explore the Array and Class object types.

Autoboxing
-----------

There may be situations when we call a method that expects an object as an
argument, but we pass it a primitive type instead (or vice versa). In these
cases, we need to convert the primitive type to an object, or convert an object
type into a primitive.

.. index:: ! boxing, ! unboxing

In older versions of Java, it was the programmer’s responsibility to convert
back and forth between primitive types and object types whenever necessary.
Converting from a primitive type to an object type was called **boxing**, and
the reverse process (object to primitive) was called **unboxing**.

.. admonition:: Examples

   **Boxing:**

   .. sourcecode:: java
      :linenos:

      int someInteger = 5;
      Integer someIntegerObject = Integer.valueOf(someInteger);
      ClassName.methodName(someIntegerObject);

   #. Line 1 declares and initializes the variable ``someInteger``.
   #. Line 2 and converts the primitive ``int`` to the ``Integer`` object type.
   #. Line 3 calls ``methodName`` and passes ``someIntegerObject`` as the
      argument. If ``methodName`` expects an object type and we tried sending
      an ``int`` instead, we would generate an error message.

   **Unboxing:**

   Let's assume that a method returns a random number of
   ``Integer`` type, and we want to combine it with a value of ``int`` type.

   .. sourcecode:: java
      :linenos:

      int ourNumber = 5;
      Integer randomNumber = ClassName.randomNumberGenerator();
      int randomInt = (int) randomNumber;
      int sum = ourNumber + randomInt;

   #. Line 2 declares and initializes ``randomNumber`` as an ``Integer`` type.
   #. Line 3 converts ``randomNumber`` to an ``int`` and stores the value in
      the ``randomInt`` variable.

.. index:: ! autoboxing

Converting between data types in order to pass values between methods quickly
became tedious and error prone. In the newer versions of Java, the compiler is
smart enough to know when to convert back and forth, and this is called
**autoboxing**.

For us, the consequence of autoboxing is that in many situations, we can use
primitive and object types interchangeably when calling methods or returning
data from those methods.

.. admonition:: Tip

   It’s a best practice to use primitives whenever possible. The primary
   exception to this occurs when storing values in collections, which we’ll
   learn about in a future lesson.

Each of the primitive data types has a corresponding object type:

#. ``int`` ---> ``Integer``
#. ``float`` ---> ``Float``
#. ``double`` ---> ``Double``
#. ``char`` ---> ``Character``
#. ``boolean`` ---> ``Boolean``

References
----------

#. `Primitive Data Types (docs.oracle.com) <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html>`__
#. `Autoboxing and Unboxing (docs.oracle.com) <http://docs.oracle.com/javase/tutorial/java/data/autoboxing.html>`__
#. `Variables (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html>`__

Check Your Understanding
-------------------------

.. admonition:: Question

   Which of the following is NOT a number data type in Java:

   #. ``number``
   #. ``int``
   #. ``float``
   #. ``double``

.. admonition:: Question

   Name the Java method responsible for checking string equality:

   #. ``.isEqualTo()``
   #. ``.sameAs()``
   #. ``.equals()``
   #. ``===``
