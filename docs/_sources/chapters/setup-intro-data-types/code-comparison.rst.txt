A Code Comparison
==================

Let’s compare a simple temperature conversion program written in both
JavaScript and Java. We want our function to convert a Fahrenheit temperature
to Celsius.

.. sourcecode:: JavaScript
   :linenos:

   const input = require('readline-sync');

   let fahrenheit = input.question("Enter the temperature in F: ");
   let celsius = (temp - 32) * (5 / 9);

   console.log(`The temperature in Celsius is: ${celsius} °C`);

Next, lets look at the Java equivalent:

.. sourcecode:: java
   :linenos:

   import java.util.Scanner;

   public class Main {
      public static void main(String[] args) {
         double fahrenheit;
         double celsius;
         Scanner in;

         in = new Scanner(System.in);
         System.out.println("Enter the temperature in F: ");
         fahrenheit = in.nextDouble();

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

In Java, you can use any class that is available without having to
import the class, but you must adhere to two very important conditions:

1. The ``javac`` and ``java`` commands must know that the class exists.
2. You must use the full name of the class

How do the ``java`` and ``javac`` commands know that certain classes
exist? We have these rules:

1. Java knows about all the classes that are defined in ``.java`` and
   ``.class`` files in your current working directory.
2. Java knows about all the classes that are shipped with java.
3. Java knows about all the classes that are included in your
   ``CLASSPATH`` environment variable. Your ``CLASSPATH`` environment
   variable can name two kinds of structures:

   1. A jar file that contains java classes. (A jar file is a “Java
      archive”, and ends in ``.jar``. For now, think of it as a zip file
      that contains a bunch of classes.)
   2. Another Unix directory that contains Java class files.

You can think of the ``import`` statement in Java as working a little
bit like the ``from module import xxx`` statement in Python. However,
behind the scenes the two statements actually do very different things.

The first important difference to understand is that the class naming
system in Java is very hierarchical. The *full* name of the Scanner
class is really ``java.util.Scanner``. You can think of this name as
having two parts: The first part ``java.util`` is called the
**package**, and the last part is the class. We’ll talk more about the
class naming system a bit later. The second important difference is that
it is the Java class loader’s responsibility to load classes into
memory, not the ``import`` statement’s.

The ``import`` statement tells the compiler that we are going to use a
shortened version of the class’s name. In this example we are going to
use the class ``java.util.Scanner``, but we can refer to it as just
``Scanner``. We could use the ``java.util.Scanner`` class without any
problem and without any import statement provided that we always
referred to it by its full name.

Don’t just trust us, try it yourself! Remove the ``import`` statement
and change ``Scanner`` to ``java.util.Scanner`` in the rest of the code.
The program should still compile and run.

Declaring Variables
--------------------

In the example above, these lines contain variable declarations:

.. code:: java

   double fahrenheit;
   double celsius;
   Scanner in;

Specifically we are saying that ``fahrenheit`` and ``celsius`` are going
to reference objects that are of type ``double``. This means that if we
were to try an assignment like ``fahrenheit = "xyz"`` the compiler would
generate an error because ``"xyz"`` is a string and ``fahrenheit`` is
supposed to be a double. The variable ``in`` will reference a Scanner
object.

For Python programmers the following error is likely to be even more
common. Suppose we forgot the declaration for ``celsius``. What would
happen if we try to manually compile our programing using
``javac TempConv.java`` on the command line?

.. code:: bash

   TempConv.java:13: cannot find symbol
   symbol  : variable celsius
   location: class TempConv
            celsius = (fahrenheit - 32) * 5.0/9.0;
            ^
   TempConv.java:14: cannot find symbol
   symbol  : variable celsius
   location: class TempConv
            System.out.println("The temperature in C is: " + celsius);
                                                             ^
   2 errors

When you see the first kind of error, where the ``^`` symbol is on the
left side of the assignment operator, it usually means that you have not
declared the variable. If you have ever tried to use a Python variable
that you have not initialized the second error message will be familiar
to you. The difference here is that we see the message before we ever
try to test our program.

.. raw:: html

   <aside class="aside-note">

When using an IDE such as IntelliJ, your code is typically checked by
the IDE’s built-in compiler as you write your code. Thus, errors are
usually visually indicated within your code by the IDE as you write your
code, saving you the extra step of having to explicitly compile your
code before finding compiler errors. Nice, huh?

.. raw:: html

   </aside>

The general rule in Java is that you must decide what kind of an object
your variable is going to reference and then you must declare that
variable before you use it. There is much more to say about the static
typing of Java but for now this is enough.

Input / Output and the Scanner Class
-------------------------------------

In the previous section we created a ``Scanner`` object. In Java,
``Scanner`` objects make getting input from the user, a file, or even
over the network relatively easy. In our case we simply want to ask the
user to type in a number at the command line, so we construct a
``Scanner`` instance by using the word ``new`` and then calling the
constructor and passing it the ``System.in`` object:

.. code:: java

   in = new Scanner(System.in);

Notice that this Scanner object is assigned to the name ``in``, which we
declared to be a ``Scanner`` earlier in the program. ``System.in`` is
similar to ``System.out`` except of course it is used for input. If you
are wondering why we must create a ``Scanner`` to read data from
``System.in`` when we can write data directly to ``System.out`` using
``println``, you are not alone. We will talk about the reasons why this
is so later when we talk in depth about Java streams. You will also see
in other examples that we can create a Scanner by passing the
``Scanner`` a ``File`` object. You can think of a ``Scanner`` as a kind
of “adapter” that makes low level objects easier to use.

.. raw:: html

   <aside class="aside-note">

As in Python, in Java you may declare and initialize your variables in
the same line: ``java     Scanner in = new Scanner(System.in);``

.. raw:: html

   </aside>

On this line we use the ``Scanner`` object to read in a number:

.. code:: java

   fahrenheit = in.nextDouble();

Here again we see the implications of Java being a strongly typed
language. Notice that we must call the method ``nextDouble``, because
the variable ``fahrenheit`` was declared as a ``double``.

As a consequence of Java’s type system, ``Scanner`` must have a function
that is guaranteed to return each kind of object it wants to be able to
read. The compiler matches up these assignment statements and if you try
to assign the results of a method call to the wrong kind of variable it
will be flagged as an error.

The table below shows you some commonly used methods of the scanner
class. There are many more methods supported by this class and we will
talk about how to find them in the next chapter.

+-----------------------+-----------------------+-----------------------+
| Return type           | Method name           | Description           |
+=======================+=======================+=======================+
| ``boolean``           | ``hasNext()``         | returns ``true`` if   |
|                       |                       | more data is present  |
+-----------------------+-----------------------+-----------------------+
| ``boolean``           | ``hasNextInt()``      | returns ``true`` if   |
|                       |                       | the next thing to     |
|                       |                       | read is an integer    |
+-----------------------+-----------------------+-----------------------+
| ``boolean``           | ``hasNextFloat()``    | returns ``true`` if   |
|                       |                       | the next thing to     |
|                       |                       | read is a float       |
+-----------------------+-----------------------+-----------------------+
| ``boolean``           | ``hasNextDouble()``   | returns ``true`` if   |
|                       |                       | the next thing to     |
|                       |                       | read is a double      |
+-----------------------+-----------------------+-----------------------+
| ``Integer``           | ``nextInt()``         | returns the next      |
|                       |                       | thing to read as an   |
|                       |                       | ``Integer``           |
+-----------------------+-----------------------+-----------------------+
| ``Float``             | ``nextFloat()``       | returns the next      |
|                       |                       | thing to read as a    |
|                       |                       | ``Float``             |
+-----------------------+-----------------------+-----------------------+
| ``Double``            | ``nextDouble()``      | returns the next      |
|                       |                       | thing to read as a    |
|                       |                       | ``Double``            |
+-----------------------+-----------------------+-----------------------+
| ``String``            | ``next()``            | returns the next      |
|                       |                       | thing to read as a    |
|                       |                       | ``String``            |
+-----------------------+-----------------------+-----------------------+
| ``String``            | ``nextLine()``        | returns the next line |
|                       |                       | read as a ``String``  |
+-----------------------+-----------------------+-----------------------+
