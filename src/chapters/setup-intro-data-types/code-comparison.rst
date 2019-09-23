A Code Comparison
==================

Let’s compare a simple temperature conversion program written in both
JavaScript and Java. We want our function to convert a Fahrenheit temperature
to Celsius.

   TODO: Convert repl.it to local code.

.. replit:: JavaScript
   :slug: NodeFtoCConverter
   :linenos:

   const input = require('readline-sync');

   let fahrenheit = input.question("Enter the temperature in °F: ");
   let celsius = (fahrenheit - 32) * (5 / 9);

   console.log(`The temperature in Celsius is: ${celsius}°C`);

Next, lets look at the Java equivalent:

.. _temp-conversion:

.. replit:: java
   :slug: JavaFtoCConverter
   :linenos:

   import java.util.Scanner;

   public class Main {
      public static void main(String[] args) {
         double fahrenheit;
         double celsius;
         Scanner input;

         input = new Scanner(System.in);
         System.out.println("Enter the temperature in °F: ");
         fahrenheit = input.nextDouble();
         input.close();

         celsius = (fahrenheit - 32) * 5/9;
         System.out.println("The temperature in Celsius is: " + celsius + "°C");
      }
   }

There are several new concepts introduced in this example. We will look
at them in the following order:

#. ``import`` statement
#.  Variable declaration
#.  Input/output and the ``Scanner`` class

``import``
-----------

You can think of the ``import`` statement in Java as working a little
bit like the ``const variableName = require('ModuleName');`` statement in
JavaScript. The ``require`` command imports the specified module, and assigns
it to ``variableName``. We can then access the class, functions, or data stored
in the module by referencing ``variableName``.

The Java ``import`` statement tells the compiler that we are going to use a
shortened version of the class name. In this example we are going to use the
class ``java.util.Scanner``, but we can refer to it as just ``Scanner``. We
could use the ``java.util.Scanner`` class without any problem and without any
import statement provided that we always referred to it by its full name.

This brings up an important distinction between Java and JavaScript. In Java,
you can use any class that is available WITHOUT having to import the class, but
you must adhere to two very important conditions:

#. The ``javac`` and ``java`` commands must know that the class exists.
#. You must use the full name of the class.

.. admonition:: Try It

   In the Java temperature conversion program, comment out the ``import``
   statement in line 1, and change ``Scanner`` on lines 7 & 9 to
   ``java.util.Scanner``. The program should still compile and run.

The class naming system in Java is very hierarchical. The *full* name of the
``Scanner`` class is really ``java.util.Scanner``. You can think of this name
as having two parts:

#. ``java.util`` is called the *package*,
#. ``Scanner`` is the class name.

We’ll talk more about the class naming system a bit later.

Java Knows Which Classes Exist, Kinda
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

How do the ``java`` and ``javac`` commands know that certain classes
exist? We have these rules:

#. Java knows about all the classes you define in the ``.java`` and ``.class``
   files in your current working directory.
#. Java knows about all the classes that get shipped with the software.
#. Java knows about all the classes included in your ``CLASSPATH`` environment
   variable. Your ``CLASSPATH`` environment variable can name two kinds of
   structures:

   a. A *Java archive file*, ``.jar``, that contains Java classes.
   b. Another Unix directory that contains Java class files.

Declaring Variables
--------------------

In the example above, these lines contain variable declarations:

.. sourcecode:: java

   double fahrenheit;
   double celsius;
   Scanner input;

Specifically we are saying that ``fahrenheit`` and ``celsius`` are going to
reference objects that are of type ``double``. This means that if we were to
try something like ``fahrenheit = "xyz"``, the compiler throws an error because
``"xyz"`` is a string and ``fahrenheit`` is supposed to be a double. The
variable ``input`` references a ``Scanner`` object.

The following error is common for new Java programmers. Suppose we forget to
include the declaration for ``celsius`` on line 6. What happens if we try to
manually compile our program using ``javac Main.java`` on the command line?

.. sourcecode:: bash

   Main.java:13: cannot find symbol
   symbol  : variable celsius
   location: class Main
            celsius = (fahrenheit - 32) * 5.0/9.0;
            ^
   Main.java:14: cannot find symbol
   symbol  : variable celsius
   location: class Main
            System.out.println("The temperature in °C is: " + celsius);
                                                             ^
   2 errors

When you see the first kind of error, where the ``^`` symbol is on the
left side of the ``=``, it usually means you have not declared the variable.

The second error message occurs when you try to use a variable that you have
not initialized with a value. These *compiler errors* occur before we ever try
to run or test our program.

.. admonition:: Note

   When using an IDE such as IntelliJ, your work is typically checked by the
   IDEs built-in compiler as you write your code. Thus, errors are often
   visually indicated by the IDE as you write. This avoids having to explicitly
   compile your code before finding errors. Nice, huh?

The general rule in Java is that you must decide what kind of object your
variable is going to reference and then declare that variable before you use
it. There is much more to say about the static typing of Java, but for now this
is enough.

.. admonition:: Note

   As in JavaScript, in Java you may declare and initialize your variables in
   the same line: ``double celsius = (fahrenheit - 32) * 5/9;``.

Input / Output and the ``Scanner`` Class
-----------------------------------------

For our temperature conversion program we created a ``Scanner`` object in line
9 and assigned it to the variable ``input``. In Java, ``Scanner`` objects make
getting input from the user, a file, or even over the network relatively easy.

In this case, we want to prompt the user to enter in a number in the command
line. We accomplish this by creating a ``Scanner`` instance using the word
``new`` and then calling the constructor and passing it the ``System.in``
object:

.. sourcecode:: java

   input = new Scanner(System.in);

Notice that this ``Scanner`` object is assigned to the name ``input``, which we
declared to be a ``Scanner`` object on line 7. ``System.in`` is similar to
``System.out`` except, as the name implies, it is used for input.

.. admonition:: Note

   If you are wondering why we must create a ``Scanner`` object to read data from
   ``System.in`` when we can write data directly to ``System.out`` using
   ``println``, you are not alone. We will talk about the reasons why this is so
   when we dive into Java streams.

On line 11 we use the ``Scanner`` object ``input`` to read in a number from the
command line:

.. sourcecode:: java

   fahrenheit = input.nextDouble();

Here again we see the implications of Java being a strongly typed language.
Notice that we must call the method ``nextDouble``, because the variable
``fahrenheit`` was declared as a ``double``.

Because Java is a statically typed language, we must call the appropriate
method on the ``Scanner`` object to ensure the entered data is of the correct
type. In this case, the compiler checks the assignment statements for
``fahrenheit`` and ``input.nextDouble()`` and throws an error if the two do not
match.

The table below shows some commonly used methods of the ``Scanner`` class.
There are many others supported by this class, and we will talk about how to
find them in the next chapter.

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
     - Returns ``true`` if the next item to read is an integer.
   * - ``hasNextFloat()``
     - ``boolean``
     - Returns ``true`` if the next item to read is a ``float``.
   * - ``hasNextDouble()``
     - ``boolean``
     - Returns ``true`` if the next item to read is a ``double``.
   * - ``nextInt()``
     - ``Integer``
     - Returns the next item to read as an ``Integer`` data type.
   * - ``nextFloat()``
     - ``Float``
     - Returns the next item to read as a ``Float`` data type.
   * - ``nextDouble()``
     - ``Double``
     - Returns the next item to read as a ``Double`` data type.
   * - ``next()``
     - ``String``
     - Returns the next item to read as a ``String`` data type.
   * - ``nextLine()``
     - ``String``
     - Returns the next line to read as a ``String`` data type.

Moving Beyond the Command Line
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You will see in other examples that we can create a ``Scanner`` object by
passing a ``File`` object as a parameter instead of ``System.in``. ``Scanner``
serves as a kind of “adapter” that makes low level objects easier to use.

Check Your Understanding
-------------------------

Lorem ipsum...
