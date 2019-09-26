Data Types
===========

Java handles values and variables differently than JavaScript, but in a similar
manner to `TypeScript chapter <https://education.launchcode.org/intro-to-professional-web-dev/chapters/typescript/variables.html>`__.

Static vs. Dynamic Typing
-------------------------

.. index:: ! dynamically typed, ! statically typed

JavaScript is a **dynamically typed** language, which means that a variable or
parameter can refer to a value of any data type (string, number, object, etc.)
at any time. When the variable is used, the interpreter figures out what type
it is and behaves accordingly.

Java is a **statically typed** language. When a variable or parameter is
declared in a statically typed language, the data type for the value must be
specified. Once the declaration is made, the variable or parameter cannot refer
to a value of any other type.

For example, this is legal in JavaScript:

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

This major difference between JavaScript and Java means that we need to pay
much more attention to types when writing Java code. Let’s begin by exploring
the most common data types in this language.

String
-------

Strings in Java and JavaScript are quite similar. Like JavaScript, Java strings
are immutable. However, unlike JavaScript, there IS a difference between using
single and double quotes around strings.

.. admonition:: Examples

   The following JavaScript declarations are all valid:

   #. ``let str = 'LaunchCode'``;
   #. ``let str = "LaunchCode"``;
   #. ``let str = 'A'``;
   #. ``let str = "A"``;

   In Java, single quotes are used around the single character data type
   ``char``. Double quotes enclose String data types:

   #. ``char charVariable = 'a'``;
   #. ``String stringVariable = "LaunchCode"``;

   The single character can be a letter, digit, punctuation, or whitespace like
   tab (``'\t'``).

Manipulating strings in Java looks similar to our experience with JavaScript,
but with a slightly different syntax. The table below summarizes the
differences between the string methods available for the two languages. For the
examples shown in the table, we will use the string variable
``String str = "Rutabaga"``.

.. list-table:: String manipulations in JavaScript vs. Java
   :header-rows: 1

   * - JavaScript
     - Java
     - Description
   * - ``str[3]``
     - ``str.charAt(3)``
     - Returns the character at index 3, (``'a'``).
   * - ``str[2:5]``
     - ``str.substring(2,4)``
     - Returns the characters from indexes 2 - 4, (``"tab"``).
   * - ``str.length``
     - ``str.length()``
     - Returns the length of the string.
   * - ``str.indexOf('a')``
     - ``str.indexOf('a')``
     - Returns the index for the first occurrence of 'a', (``3``).
   * - ``str.split('delimiter')``
     - ``str.split('delimiter')``
     - Splits the string into sections at each ``delimiter`` and stores the
       sections as elements in an array.
   * - ``str.concat(string2, string3, ...)``
     - ``str.concat(string2).concat(string3)``
     - In Java, ``concat`` concatenates only two strings. To join multiple
       strings, method chaining is required.
   * - ``str.trim()``
     - ``str.trim()``
     - Removes any whitespace at the beginning or end of the string.
   * - ``str.toUpperCase(), str.toLowerCase()``
     - ``str.toUpperCase(), str.toLowerCase()``
     - Changes all alphabetic characters in the string to UPPERCASE or
       lowercase, respectively.
   * - ``str.includes("text")``
     - ``str.contains("text")``
     - Searches for the specified text within a string and returns ``true`` or
       ``false``.
   * - ``str === otherString``
     - ``str.equals(otherString)``
     - Compares strings for equality and returns a boolean. Java does NOT have
       a corresponding operator for the strict equality ``===`` used in JavaScript.

Primitive Types
----------------

In the `More on Types <https://education.launchcode.org/intro-to-professional-web-dev/chapters/more-on-types/index.html>`__
chapter from unit 1, you learned about 5 primitive data types used by
JavaScript.

#. Strings
#. Numbers
#. Booleans
#. ``undefined``
#. ``null``

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

Java uses 3 primitive data types to express different types of numbers, whereas
JavaScript captures all of these in the ``number`` type.

.. admonition:: Warning

   As we will see in a later section, the ``float`` data type sacrifices some
   accuracy for speed of calculation. Thus, evaluating 1.11111 + 3 results in an
   answer of 4.1111097 instead of 4.11111.

   Anytime you need to perform calculations with decimal values, consider using
   the ``double`` type instead of ``float``.

Primitive data types are *immutable* and can be combined to build larger data
structures like arrays and objects. One example is combining multiple ``char``
to form a ``String`` data type.

Autoboxing
^^^^^^^^^^^

In older versions of Java it was the programmer’s responsibility to
convert back and forth from a primitive to an object whenever necessary.
This involved converting a value of a primitive type to an object type,
or vice versa. It looked like this:

.. sourcecode:: java
   :linenos:

   int x = 5;
   Integer y = Integer.valueOf(x);
   int z = (int) y;

This processing of converting a primitive to an object (e.g.
``Integer y = Integer.valueOf(x)``) was called **boxing**. The reverse
process (e.g. ``int z = (int) y``) is called **unboxing**. In Java 5,
the compiler became smart enough to know when to convert back and forth.
This process is called **autoboxing**. The consequence of autoboxing for
the Java programmer is that in many situations you can use primitive and
object types interchangeably.

.. admonition:: Tip

   It’s a best practice to use primitives whenever possible. The primary
   exception to this occurs when storing values in collections, which we’ll
   learn about in a future lesson.

.. _references-1:

References
----------

-  `Primitive Data Types
   (docs.oracle.com) <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html>`__
-  `Autoboxing and Unboxing
   (docs.oracle.com) <http://docs.oracle.com/javase/tutorial/java/data/autoboxing.html>`__
-  `Variables
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html>`__
-  `Arrays
   (docs.oracle.com) <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html>`__
