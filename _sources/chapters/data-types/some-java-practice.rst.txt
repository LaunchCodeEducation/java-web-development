Some Java Practice
===================

Let’s move beyond our "Hello, World" example and explore a simple temperature
conversion program. We want our function to convert a Fahrenheit temperature to
Celsius.

.. _temp-conversion:

Temperature Conversion
-----------------------

#. Open the ``TempConverter`` file in the ``java-web-dev-exercises`` project in IntelliJ.

   .. figure:: figures/tempConverterTree.png
      :alt: The ``TempConverter`` file

      The ``TempConverter`` file

#. Here's what the file should look like. We will analyze the different statements 
   in a moment.

   .. sourcecode:: java
      :linenos:

      package org.launchcode.java.demos.lsn1datatypes;

      import java.util.Scanner;

      public class TempConverter {
         public static void main(String[] args) {
            double fahrenheit;
            double celsius;
            Scanner input;

            input = new Scanner(System.in);
            System.out.println("Enter the temperature in Fahrenheit: ");
            fahrenheit = input.nextDouble();
            input.close();

            celsius = (fahrenheit - 32) * 5/9;
            System.out.println("The temperature in Celsius is: " + celsius + "°C");
         }
      }

#. Build and run the program to verify that it works. Entering a Fahrenheit
   temperature of ``212`` yields the result, ``The temperature in Celsius is:
   100.0°C``.

There are several new concepts introduced in this example. We will look
at them in the following order:

#. Java packages
#. The ``import`` statement
#. Declaring variables
#. Collecting input with the Scanner class

.. _java-packages:

.. index:: ! encapsulation

Java Packages
-------------

Line 1 of of the program above, ``package org.launchcode.java.demos.lsn1datatypes;``
declares the package in which the file resides. For this simple program, your code 
could run without this line. However, you want to get used to always declaring the 
package of your Java classes. 

Packages help to **encapsulate** your code. Encapsulation refers to the practice of 
shielding your code from outside influences. It's an essential component of good 
object oriented programming, and package declaration in Java is just one application 
of this principle. Without declaring a package, a Java class exists within the default 
package. In larger applications, leaving all classes in the default package risks naming
conflicts and bugs.

.. _import-statement:

``import``
-----------

The ``import`` statement in Java allows us to access the class, methods, and
data stored a different file. ``import`` tells the compiler that we are going
to use a shortened version of the class name. In this example, we are going to
use the class ``java.util.Scanner``, but we can refer to it as just
``Scanner``. We could use the ``java.util.Scanner`` class without any problem
and without any import statement, provided that we always refer to it by its
full name.

This idea bears repeating. In Java, you can use any available class
WITHOUT having to import it, but you must use the full name of the class.
"Available" classes include:

#. All the classes you define in the ``.java`` and ``.class`` files in your
   current working directory.
#. All the classes that get shipped with the software.

.. admonition:: Try It

   In the sample code, remove the ``import`` statement in line 3, and change
   ``Scanner`` on lines 9 & 11 to ``java.util.Scanner``. The program should
   still compile and run.

The class naming system in Java is very hierarchical. The *full* name of the
``Scanner`` class is really ``java.util.Scanner``. You can think of this name
as having two parts:

#. ``java.util`` is called the *package*,
#. ``Scanner`` is the class name.

We’ll talk more about the class naming system a bit later.

.. _declaring-variables:

Declaring Variables
--------------------

In the example above, lines 7 - 9 contain variable declarations:

.. sourcecode:: java
   :lineno-start: 7

   double fahrenheit;
   double celsius;
   Scanner input;

Since Java is a statically typed language, we must always declare the data type
for any variable. Lines 7 & 8 establish that ``fahrenheit`` and ``celsius``
will hold values of type ``double``. In line 9, the variable ``input``
references a ``Scanner`` object.

If later in the code we try to initialize ``fahrenheit`` with a string:

.. sourcecode:: java

   fahrenheit = "xyz"

the compiler throws an error because ``fahrenheit`` is declared to be a double.

The following error is common for new Java programmers. Suppose we forget to
include the declaration for ``celsius``. What happens when we try to
compile and run our program?

.. admonition:: Try It

   #. Edit your ``TempConverter`` class by removing line 8, which declares the
      variable ``celsius``.
   #. Click any of the "Run" options in IntelliJ. Alternatively, use the
      terminal to navigate to the parent directory of your
      ``TempConverter.java`` class and run ``java TempConverter.java``.

Your terminal will return some errors that resemble these:

.. sourcecode:: bash

   Error:(16, 9) java: cannot find symbol
   symbol:   variable celsius
   location: class TempConverter

   Error:(17, 64) java: cannot find symbol
   symbol:   variable celsius
   location: class TempConverter

These two *compiler errors* occur before the program runs. The values in the
parentheses ``()`` give the line number and text column where the error was
found. In the first description (line 16, column 9), the ``celsius`` variable
before the ``=`` is flagged. When this type of error happens, it usually means
that the variable was not declared before we tried to initialize it with a
value.

The second error message (line 17, column 64) occurs because we use
``celsius`` before it has been assigned a value.

.. admonition:: Note

   When using an IDE such as IntelliJ, your work is typically checked by the
   IDEs built-in compiler as you write your code. Errors are often visually
   indicated by the IDE as you type. This avoids having to explicitly
   compile your code before finding errors. Nice, huh?

   .. figure:: figures/IDE-flagged-errors.png
      :alt: The ``celsius`` variables are flagged.

      The red coloring of the ``celsius`` variables indicate errors.

The general rule in Java is that you must decide on the data type for your
variable first, and then declare that variable before you use it. There is much
more to say about the static typing of Java, but for now this is enough.

.. admonition:: Note

   As in other languages, Java allows you to declare and initialize your
   variables in the same line:

   .. sourcecode:: java

      double celsius = (fahrenheit - 32) * 5/9;

Add Comments to Your Code
--------------------------

As programs get bigger and more complicated, they get more difficult to read.
Good programmers try to make their code understandable to others, but it is
still tricky to look at a large program and figure out what it is doing and
why.

Also, there are times when programmers need to isolate or ignore certain
portions of their code as they are testing it. In the "Try It" box above, you
were instructed to *remove* a line of code in order to create compiler errors.
However, programmers are usually reluctant to delete lines that they might need
to bring back.

.. index:: ! comments

Best practice encourages us to add **comments** to our programs. These are
notes that clearly explain what the code is doing.

A comment is text within a program intended only for a human reader—--it is
completely ignored by the compiler or interpreter. In Java, the ``//`` token
indicates the start of a comment, and the rest of the line gets ignored. For
comments that stretch over multiple lines, the text falls between the symbols
``/*   */``.

Comments can also be used to temporarily skip a portion of the code when a
program runs. Instead of removing ``double celsius;`` in ``TempConverter``, we
could *comment out* the line. This would create the same compiler errors we
wanted to witness, but it would preserve the original code and allow us to
easily reactivate it by removing the ``//`` token from the line.

.. admonition:: Example

   .. sourcecode:: java
      :linenos:

      import java.util.Scanner;

      // Here is an example of a comment.

      /* Here is how
      to have
      multi-line
      comments. */

      /*
      Or
      like
      this.
      */

      public class HelloWorld {
         public static void main(String[] args) {
            Scanner input; // Comments do not have to start at the beginning of a line.

            input = new Scanner(System.in);
            System.out.println("Please enter your first name: ");
            String name = input.next(); //Declares the 'name' variable and initializes it with text from the command line.
            input.close();

            System.out.println("Hello, " + name + "!");

            // System.out.println("This line will NOT print!");
         }
      }

.. _scanner-input:

Collect Input with the ``Scanner`` Class
-----------------------------------------

In Java, ``Scanner`` objects make getting input from the user, a file, or even
over the network relatively easy. For our temperature conversion program, we
declared the variable ``input`` to be of type ``Scanner``.

.. sourcecode:: java
   :lineno-start: 9

   Scanner input;

We want our program to prompt the user to enter in a number in the command
line. We accomplish this by creating a ``Scanner`` instance using the word
``new`` and then calling the constructor and passing it the ``System.in``
object:

.. sourcecode:: java
   :lineno-start: 11

   input = new Scanner(System.in);

Notice that this ``Scanner`` object is assigned to the name ``input``, which we
declared to be a ``Scanner`` object earlier. 

And you know those ``System`` statements we've been using? Like ``System.in`` above
here, and ``System.out.println()`` for print statements. Well, ``System`` itself is 
a java class. ``System.in`` is similar to ``System.out`` except, as the name 
implies, it is used for input.

.. admonition:: Note

   If you are wondering why we must create a ``Scanner`` object to read data from
   ``System.in`` when we can write data directly to ``System.out`` using
   ``println``, you are not alone. We will talk about the reasons why this is so
   when we dive into Java streams.

Next, line 12 asks the user to enter a number, and in line 13 we use ``input``
to read the value from the command line:

.. sourcecode:: java
   :lineno-start: 12

   System.out.println("Enter the temperature in Fahrenheit: ");
   fahrenheit = input.nextDouble();

Here again we see the implications of Java being a strongly typed language.
Notice that we must call the method ``nextDouble``, because the variable
``fahrenheit`` was declared as a ``double``.

Because Java is a statically typed language, we must call the appropriate
method on the ``Scanner`` object to ensure the entered data is of the correct
type. In this case, the compiler compares the types for ``fahrenheit`` and
``input.nextDouble()`` and throws an error if the two do not match.

The table below shows some commonly used methods of the ``Scanner`` class.
There are many others supported by this class, and the `Oracle website <https://docs.oracle.com/javase/10/docs/api/java/util/Scanner.html>`__
provides a complete listing of the ``Scanner`` methods.

.. list-table:: ``Scanner`` methods
   :header-rows: 1

   * - Method Name
     - Return Type
     - Description
   * - ``hasNext()``
     - ``boolean``
     - Returns ``true`` if more data is present.
   * - ``hasNextInt()``
     - ``boolean``
     - Returns ``true`` if the next item to read is an ``int`` data type.
   * - ``hasNextFloat()``
     - ``boolean``
     - Returns ``true`` if the next item to read is a ``float`` data type.
   * - ``hasNextDouble()``
     - ``boolean``
     - Returns ``true`` if the next item to read is a ``double`` data type.
   * - ``nextInt()``
     - ``int``
     - Returns the next item to read as an ``int`` data type.
   * - ``nextFloat()``
     - ``float``
     - Returns the next item to read as a ``float`` data type.
   * - ``nextDouble()``
     - ``double``
     - Returns the next item to read as a ``double`` data type.
   * - ``next()``
     - ``String``
     - Returns the next item to read as a ``String`` data type.
   * - ``nextLine()``
     - ``String``
     - Returns the next line to read as a ``String`` data type.

Closing ``Scanner``
^^^^^^^^^^^^^^^^^^^^

To collect data from the command line or other source, create a ``Scanner``
object. This opens up resources in your machine to manage the input, and these
resources remain open even after the required data is loaded into your program.

Leaving a ``Scanner`` open is like keeping a window open in your house 24/7.
Anyone can climb into your home, and you lose $$$ by trying to heat and cool
your space while it is open to the outside air. Similarly, an open ``Scanner``
can allow unintended access to your program, and it ties up resources that
might be needed elsewhere.

Best practice states that if you open a ``Scanner`` object, close it after
it finishes its job. Line 14 does this in our ``TempConverter`` program:

.. sourcecode:: java
   :lineno-start: 14

   input.close();

The general syntax is ``scannerObjectName.close()``.

Moving Beyond the Command Line
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ``Scanner`` class serves as a kind of adapter that gathers primitive data
types as input and converts them into object types (e.g. it converts an ``int``
into ``Integer``). We will discuss the purpose of this later, but for now,
know that this adaptation makes low-level data types easier to use.

For the temperature conversion program, we collected user input from the
command line, but there are other options for collecting data for our programs.
In future examples, we will create a ``Scanner`` object by passing a ``File``
object as a parameter instead of ``System.in``.

Check Your Understanding
-------------------------

.. admonition:: Question

   An ``import`` statement is required to use a Java class defined in another
   package.

   #. True
   #. False

.. admonition:: Question

   Which of the following ``Scanner`` methods should you use to return an
   expected ``String`` input? Check ALL that apply.

   #. ``.hasNext()``
   #. ``.nextLine()``
   #. ``.next()``
   #. ``.nextFloat()``

