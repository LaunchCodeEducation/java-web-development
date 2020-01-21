.. _array-list:

ArrayList
=========

To write an **ArrayList** version of the program, we will have to introduce
several new Java concepts, including the class ``ArrayList``. We will also
review different kinds of ``for`` loops used in Java.

Before going any further, we suggest you run the ``ArrayListGradebook``
program in IntelliJ. You can view this program in ``java-web-dev-exercises``.
Once you’ve done that, let’s look at what is happening in the Java
source code.

.. sourcecode:: java
   :linenos:

   package org.launchcode.java.demos.collections;

   import java.util.ArrayList;
   import java.util.Scanner;

   public class ArrayListGradebook {

      public static void main(String[] args) {

         ArrayList<String> students = new ArrayList<>();
         ArrayList<Double> grades = new ArrayList<>();
         Scanner input = new Scanner(System.in);
         String newStudent;

         System.out.println("Enter your students (or ENTER to finish):");

         // Get student names
         do {
            newStudent = input.nextLine();

            if (!newStudent.equals("")) {
               students.add(newStudent);
            }

         } while(!newStudent.equals(""));

         // Get student grades
         for (String student : students) {
            System.out.print("Grade for " + student + ": ");
            Double grade = input.nextDouble();
            grades.add(grade);
         }

         // Print class roster
         System.out.println("\nClass roster:");
         double sum = 0.0;

         for (int i = 0; i < students.size(); i++) {
            System.out.println(students.get(i) + " (" + grades.get(i) + ")");
            sum += grades.get(i);
         }

         double avg = sum / students.size();
         System.out.println("Average grade: " + avg);
      }
   }


.. index:: ! ArrayList

Here we declare and initialize two objects, ``students`` and ``grades``,
which appear to be of type ``ArrayList<String>`` and
``ArrayList<Double>``, respectively. An ``ArrayList`` in Java is very
similar to an :ref:`Array <array>`. Like an ``Array``, we must let
the compiler know what kind of objects our ``ArrayList`` is going to
contain. In the case of ``students``, the ``ArrayList`` will contain
values of type
``String`` (representing the names of the students), so we use the
``ArrayList<String>`` syntax to inform the compiler that we intend to
fill our list with Strings. Similarly, ``grades`` will hold exclusively
values of type ``Double`` and is declared to be of type
``ArrayList<Double>``.

.. admonition:: Warning

   Notice that we declared ``grades`` to be of type ``ArrayList<Double>``,
   using the wrapper class ``Double`` rather than the primitive type
   ``double``. All values stored in Java collections must be objects, so
   we’ll have to use object types in those situations.

In lines 10 and 11, we also initialize each list by creating a new, empty
list. Note that when we call the ``ArrayList`` constructor, as in
``new ArrayList<>()``, we don’t need to specify type (it’s implicit in the
left-hand side of the assignment).

.. index:: ! generic class, generic type

.. admonition:: Note

   You will sometimes see the ``ArrayList`` class written as ArrayList<E>,
   where ``E`` represents a placeholder for the type that a programmer will
   declare a given list to hold. This is especially true in documentation.
   You can think of ``E`` as representing an arbitrary type.

   Classes like ArrayList<E> that take another type or class as a parameter
   are referred to as **generic classes** or **generic types**.

``ArrayList`` Iteration
-----------------------

``do-while``
^^^^^^^^^^^^

We then use a ``do-while`` loop to collect the names of each of the students
in the class.

.. sourcecode:: java
   :lineno-start: 18

   // Get student names
   do {
      newStudent = input.nextLine();

      if (!newStudent.equals("")) {
         students.add(newStudent);
      }

   } while(!newStudent.equals(""));

Recall that a ``do-while`` loop is very similar to a ``while`` loop, but the
execution condition is checked at the end of the loop block. This has the net
effect that the code block will always run at least once. In this example, we
prompt the user for a name, which Java processes via ``input.nextLine()`` when
the user hits the enter key. To finish entering names, the user enters a blank
line.

.. index:: ! ArrayList.add()

For each student that is entered (that is, each non-empty line), we add
the new ``String`` to the end of our list with ``students.add(newStudent)``.
The ``.add()`` method is provided by the `ArrayList
Class <http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html>`__.
There are lots of other ArrayList methods to get familiar with, some of which
we will discuss in more detail below.

Note that our program imports ``java.util.ArrayList`` to take advantage of this
Java provided class.

``for-each``
^^^^^^^^^^^^

Below the ``do-while`` loop are two different loops that demonstrate two ways
you can loop through a list in Java. Here’s the first, which collects the
numeric grade for each student:

.. sourcecode:: java
   :lineno-start: 27

   // Get student grades
   for (String student : students) {
      System.out.print("Grade for " + student + ": ");
      Double grade = input.nextDouble();
      grades.add(grade);
   }

This, you may recall, is Java's ``for-each`` loop syntax. You may read this
in your head, or even aloud, as: ``for each student in students``. As you might
expect at this point, we must declare the iterator variable ``student``
with its data type.

``for``
^^^^^^^
The next loop on display prints out each student’s name and grade:

.. sourcecode:: java
   :lineno-start: 34

   // Print class roster
   System.out.println("\nClass roster:");
   double sum = 0.0;

   for (int i = 0; i < students.size(); i++) {
      System.out.println(students.get(i) + " (" + grades.get(i) + ")");
      sum += grades.get(i);
   }

.. index:: ! ArrayList.size()

Here, we introduce the syntax ``students.size()`` which utilizes the ``size()``
method of ``ArrayList``. This method returns the integer representing the
number of items in the list. This is similar to String's ``.length()``
:ref:`method <string-methods>`.

In this ``for`` loop, we use a *loop index* to define the starting point,
ending point, and increment for iteration. It may be helpful for you to
consider this kind of construction as something like,  ``for integer i in the
range of the number of items in students...``. The first statement inside the
parenthesis declares and initializes a loop index variable ``i``. The second
statement is a Boolean expression that is our exit condition. In other words,
we will keep looping as long as this expression evaluates to ``true``. The
third statement is used to increment the value of the loop index variable at
the end of iteration through the loop.

Again, the syntax ``i++`` is Java shorthand for ``i = i + 1``. Java also
supports the shorthand ``i--`` to decrement the value of ``i``.
We can also write ``i += 2`` as shorthand for ``i = i + 2``.

In the final lines of the program, we compute the average grade for all
students:

.. sourcecode:: java
   :lineno-start: 43

   double avg = sum / students.size();
   System.out.println("Average grade: " + avg);

ArrayList Methods
-----------------

Let’s gather up a few of the ``ArrayList`` methods that we’ve encountered so
far, along with a few new ones. While these will be the most common methods and
properties that you use with this class, they by no means represent a complete
list. Refer to the `official documentation on the ArrayList
class <http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html>`__
for such a list, and for more details.

To demonstrate the use of these methods, we'll create a new ``ArrayList``
called ``planets``.

.. sourcecode:: java

   ArrayList<String> planets = new ArrayList<>();

Ok, we've got an empty ArrayList. We need to use the class's ``.add()`` method
to populate this collection with items.

.. note::

   There are other means to declare and initialize an ArrayList in fewer lines.
   These require knowledge of other collections types, so we'll stick with ``.add()``
   for the time being.

Using ``.add()`` to populate ``planets``:

.. sourcecode:: java
   :linenos:

   planets.add("Mercury");
   planets.add("Venus");
   planets.add("Earth");
   planets.add("Mars");
   planets.add("Jupiter");
   planets.add("Saturn");
   planets.add("Uranus");
   planets.add("Neptune");

Thus, the first item in this table:

.. _arraylist-methods:

.. list-table:: ArrayList methods in Java
   :header-rows: 1

   * - Java Syntax
     - Description
     - Example
   * - ``add()``
     - Adds an item to the ArrayList
     - ``planets.add("Pluto")`` adds ``Pluto`` to ``planets``
   * - ``size()``
     - Returns the number of items in an ArrayList, as an ``int``
     - ``planets.size()`` returns ``9``
   * - ``contains()``
     - Checks to see if the ArrayList contains a given item, returning a Boolean
     - ``planets.contains("Earth")`` returns ``true``
   * - ``indexOf()``
     - Looks for an item in an ArrayList, returns the index of the first occurrence of the item if it exists, returns -1 otherwise
     - ``planets.indexOf("Jupiter")`` returns ``4``

Here's a couple more methods that require slightly longer descriptions:

.. _arraylistsort:

.. list-table:: Collections.sort()
   :header-rows: 1

   * - Java Syntax
     - Description
     - Example
   * - ``Collections.sort()``
     - Rearranges the elements of a ``Collection`` into ascending order.
     - ``Collections.sort(planets)`` produces ``["Earth", "Jupiter", "Mars", "Mercury", "Neptune", "Pluto", "Saturn", "Uranus", "Venus"]``

This method is technically used on Java's ``Collections`` class and
thus requires a different ``import`` statement:

.. sourcecode:: java

   import java.util.Collections;

``Collections`` is itself a member of the collections framework but not all
members of the framework are instances of this class. We include this method
here because, should you be in the market for a sorting method, this is a
helpful one to know.

.. list-table:: toArray()
   :header-rows: 1

   * - Java Syntax
     - Description
     - Example
   * - ``toArray()``
     - Returns an Array containing the elements of the ArrayList
     - ``planets.toArray(planetsArray)`` returns
       ``{"Earth", "Jupiter", "Mars", "Mercury", "Neptune", "Pluto", "Saturn", "Uranus", "Venus"}``

Perhaps you recall that in Java, you must know the size of the Array when you
create it. So we'll need to first define the new Array before we can use
``toArray()``.

.. sourcecode:: java
   :linenos:

   String[] planetsArray = new String[planets.size()];
   planets.toArray(planetsArray);

Speaking of Arrays, let's see the Array version of Gradebook next.

References
----------

-  `Java Collections
   (docs.oracle.com) <http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html>`__
-  `ArrayList Class
   (docs.oracle.com) <http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html>`__

Check Your Understanding
-------------------------

.. admonition:: Question

   The number of entries in an ``ArrayList`` may not be modified.

   #. True
   #. False

.. ans: False

.. admonition:: Question

   Create an ``ArrayList`` called ``charStars`` containing ``a``, ``b``, and ``c``.

   #.

      .. sourcecode:: java
         :linenos:

         ArrayList<String> charStars = new ArrayList<>();
         charStars.add('a');
         charStars.add('b');
         charStars.add('c');

   #.
      .. sourcecode:: java
         :linenos:

         ArrayList<Char> charStars = new ArrayList<>();
         charStars.add('a');
         charStars.add('b');
         charStars.add('c');

   #.
      .. sourcecode:: java

         ArrayList<char> charStars = new ArrayList<char>('a', 'b', 'c');

   #.
      .. sourcecode:: java
         :linenos:

         ArrayList<String> charStars = new ArrayList<>();
         charStars.add("a");
         charStars.add("b");
         charStars.add("c");

.. ans: ArrayList<String> charStars = new ArrayList<>();
         charStars.add("a");
         charStars.add("b");
         charStars.add("c");
