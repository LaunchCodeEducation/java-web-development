.. index:: ! data structure

Data Structures
===============

A **data structure** is a programming construct to
aggregate lots of values into one value. More simply, a data structure
lets us hold on to lots of data in a single place. Many types of data
structures exist in various languages. A few examples are lists, dictionaries, 
arrays, tuples, etc.

Java provides powerful and flexible structures to store data, known as
`collections <http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html>`__.
We’ll introduce only a few here, but they will be sufficient for all of
our basic needs while we get going with Java.

Ordered Data: Lists and Arrays
------------------------------

We’ll explore collections in Java by looking at different versions of
the same program. The program functions as a gradebook, allowing a
user (a professor or teacher) to enter the class roster for a course,
along with each student’s grade. It then prints the class roster along
with the average grade. In each variation of this program, the grading
system could be anything numeric, such as a 0.0-4.0 point scale, or a
0-100 percentage scale.

A test run of the program might yield the following:

.. sourcecode:: bash

   Enter your students (or ENTER to finish):
   Chris
   Jesse
   Sally

   Grade for Chris: 3.0
   Grade for Jesse: 4.0
   Grade for Sally: 3.5

   Class roster:
   Chris (3.0)
   Jesse (4.0)
   Sally (3.5)

   Average grade: 3.5

We’ll look at the gradebook using an ``Arraylist`` first. 

Gradebook (Java ArrayList Version)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To write this program, we will have to introduce
several new Java concepts, including the class ``ArrayList``. We will also review different 
kinds of for loops used in Java.

.. sourcecode:: java

   package org.launchcode.java.demos.collections;

   import java.util.ArrayList;
   import java.util.Scanner;

   public class Gradebook {

       public static void main(String[] args) {

           ArrayList<String> students = new ArrayList<>();
           ArrayList<Double> grades = new ArrayList<>();
           Scanner in = new Scanner(System.in);
           String newStudent;

           System.out.println("Enter your students (or ENTER to finish):");

           // Get student names
           do {
               newStudent = in.nextLine();

               if (!newStudent.equals("")) {
                   students.add(newStudent);
               }

           } while(!newStudent.equals(""));

           // Get student grades
           for (String student : students) {
               System.out.print("Grade for " + student + ": ");
               Double grade = in.nextDouble();
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

Before going any further, we suggest you run the above program in
IntelliJ. You can view this program in ``java-web-dev-exercises``.

Once you’ve done that, let’s look at what is happening in the Java
source code.

.. sourcecode:: java

   ArrayList<String> students = new ArrayList<>();
   ArrayList<Double> grades = new ArrayList<>();
   Scanner in = new Scanner(System.in);
   String newStudent;

.. index:: ! ArrayList

Here we declare and initialize two objects, ``students`` and ``grades``,
which appear to be of type ``ArrayList<String>`` and
``ArrayList<Double>``, respectively. An **ArrayList** in Java is very
similar to an :ref:`Array <array>`. Like an ``Array``, we must let
the compiler know what kind of objects our ``ArrayList`` is going to 
contain. In the case of ``students``, the ``ArrayList`` will contain 
values of type
``String`` (representing the names of the students), so we use the
``ArrayList<String>`` syntax to inform the compiler that we intend to
fill our list with Strings. Similarly, ``grades`` will hold exclusively
values of type ``Double`` and is declared to be of type
``ArrayList<Double>``.

.. warning:: 

   Notice that we declared ``grades`` to be of type ArrayList<Double>,
   using the wrapper class ``Double`` rather than the primitive type
   ``double``. All values stored in Java collections must be objects, so
   we’ll have to use object types in those situations. 


We then initialize each list by creating a new, empty list. Note that
when we call the ``ArrayList`` constructor, as in ``new ArrayList<>()``,
we don’t need to specify type (it’s implicit in the left-hand side of
the assignment).

.. index:: ! generic class, generic type

.. note:: 

   You will sometimes see the ``ArrayList`` class written as ArrayList<E>,
   where ``E`` represents a placeholder for the type that a programmer will
   declare a given list to hold. This is especially true in documentation.
   You can think of ``E`` as representing an arbitrary type.

   Classes like ArrayList<E> that take another type or class as a parameter
   are referred to as **generic classes** or **generic types**.


We then use a ``do-while`` loop to collect the names of each of the students
in the class.

.. sourcecode:: java

   // Get student names
   do {
       newStudent = in.nextLine();

       if (!newStudent.equals("")) {
           students.add(newStudent);
       }

   } while(!newStudent.equals(""));

Recall that a do-while loop is very similar to a while loop, but it has
its check at the end of the loop block. This has the net effect that
we’ll always run the block at least once. In this example, we prompt the
user for a name, which we read in via ``in.nextLine()`` when they hit
the enter key. To finish entering names, they enter a blank line.

For each student that is entered (that is, each non-empty line), we add
the new string to the end of our list with ``students.add(newStudent)``.
The ``.add()`` method is a method provided by the `ArrayList
Class <http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html>`__.
There are lots of other list methods.

Below the do-while loop are two different for loops that demonstrate the
two ways you can loop through a list in Java. Here’s the first, which
collects the numeric grade for each student:

.. code:: java

   // Get student grades
   for (String student : students) {
       System.out.print("Grade for " + student + ": ");
       Double grade = in.nextDouble();
       grades.add(grade);
   }

This for loop syntax is very similar to that of Python, where the
analogous loop would begin: ``for student in students:``. As you might
expect at this point, we must declare the iterator variable ``student``
in Java, which was not explicitly done in Python.

The other for loop on display prints out each student’s name and grade:

.. code:: java

   // Print class roster
   System.out.println("\nClass roster:");
   double sum = 0.0;

   for (int i = 0; i < students.size(); i++) {
       System.out.println(students.get(i) + " (" + grades.get(i) + ")");
       sum += grades.get(i);
   }

In this loop, we use a *loop index*, a different style of for loop. We
also introduce the syntax ``students.size()`` which utilizes the
``ArrayList``\ ’s ``size()`` method to return the integer representing
the number of items in the list.

The syntax of this for loop may look strange to you, but in fact it is
not too different from what happens in Python using ``range``. The
syntax ``for (int i = 0; i < students.size(); i++)`` is exactly
equivalent to the Python ``for i in range(len(students))``. The first
statement inside the parenthesis declares and initializes a loop index
variable ``i``. The second statement is a Boolean expression that is our
exit condition. In other words, we will keep looping as long as this
expression evaluates to true. The third statement is used to increment
the value of the loop index variable at the end of iteration through the
loop. The syntax ``i++`` is Java shorthand for ``i = i + 1``. Java also
supports the shorthand ``i--`` to decrement the value of ``i``. Like
Python, you can also write ``i += 2`` as shorthand for ``i = i + 2``.

In the final lines of the program, we compute the average grade for all
students:

.. code:: java

   double avg = sum / students.size();
   System.out.println("Average grade: " + avg);

ArrayList Methods and Properties
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Let’s gather up a few of the ``ArrayList`` methods and properties that
we’ve encountered so far, along a few new ones. While these will be the
most common methods and properties that you use with this class, they by
no means represent a complete list. Refer to the `official documentation
on the ``ArrayList``
class <http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html>`__
for such a list, and for more details.

+------------+---------------------------------+-----------------------+
| Name       | Description                     | Example               |
+============+=================================+=======================+
| ``size``   | Represents the number of items  | ``students.size()``   |
|            | in the list, as an ``int``      |                       |
+------------+---------------------------------+-----------------------+
| ``add``    | Adds an item to the list        | ``students.add("Sally |
|            |                                 | ")``                  |
+------------+---------------------------------+-----------------------+
| ``contains | Checks to see if the list       | ``students.contains(" |
| ``         | contains a given item,          | Haley")``             |
|            | returning a boolean             |                       |
+------------+---------------------------------+-----------------------+
| ``indexOf` | Looks for an item in a list,    | ``students.indexOf("Z |
| `          | returns the index of the first  | ach")``               |
|            | occurrence of the item if it    |                       |
|            | exists, returns -1 otherwise    |                       |
+------------+---------------------------------+-----------------------+
| ``sort``   | Sorts a list, using the         | ``students.sort()``   |
|            | “default” sort comparison       |                       |
+------------+---------------------------------+-----------------------+
| ``toArray` | Returns an array containing the | ``students.toArray()` |
| `          | elements of the list            | `                     |
+------------+---------------------------------+-----------------------+

Gradebook (Java Array Version)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We were introduced to arrays in Java in a previous lesson, so let’s
spend a moment comparing them to lists. As we noted at that beginning of
this section, we are going to use the Java ``ArrayList`` type to store
simple sets of data. They are easy to use and more closely match the way
that Python lists behave.

Why does Java have both arrays and ``ArrayList``? The answer is
historical, at least in part. Java is a C-style language, and arrays are
the most basic data structure in C. Additionally, using an array over an
``ArrayList`` might be preferred in some circumstances, primarily for
performance reasons (array operations are generally faster than list
operations). Also note that *arrays are of fixed size*. You can not
expand or contract an array after it is created, so you must know
exactly how many elements it will need to hold when you create it. This
fact is reason enough to use lists in most scenarios.

To illustrate array usage, here is a version of the gradebook program
that uses arrays instead of lists:

.. code:: java

   package org.launchcode.java.demos.java4python;

   import java.util.ArrayList;
   import java.util.Scanner;

   public class GradebookArray {

       public static void main(String[] args) {

           // Allow for at most 30 students
           int maxStudents = 30;

           String[] students = new String[maxStudents];
           double[] grades = new double[maxStudents];
           Scanner in = new Scanner(System.in);

           String newStudent;
           int numStudents = 0;

           System.out.println("Enter your students (or ENTER to finish):");

           // Get student names
           do {
               newStudent = in.nextLine();

               if (!newStudent.equals("")) {
                   students[numStudents] = newStudent;
                   numStudents++;
               }

           } while(!newStudent.equals(""));

           // Get student grades
           for (int i = 0; i < numStudents; i++) {
               System.out.print("Grade for " + students[i] + ": ");
               double grade = in.nextDouble();
               grades[i] = grade;
           }

           // Print class roster
           System.out.println("\nClass roster:");
           double sum = 0.0;

           for (int i = 0; i < numStudents; i++) {
               System.out.println(students[i] + " (" + grades[i] + ")");
               sum += grades[i];
           }

           double avg = sum / numStudents;
           System.out.println("Average grade: " + avg);
       }

   }

Note that we have to decide up front how large our arrays ``students``
and ``grades`` are going to be. Thus, it is advisable to make the arrays
potentially larger than they need to be. Like lists, we can index into
arrays with integers (``students[i]`` for example). Unlike lists,
however, there is no analog of ``.add()``, which adds an item to “the
end” of a list. We must always access and assign array elements using an
explicit index. This makes for code that can seem littered with array
counters (like our friends ``i`` and ``j``) and is more difficult to
read (not to mention more error-prone).

Like lists, however, we can loop through an array using a ``for-each``
loop as long as we don’t need to use the index of the current item. If
we only wanted to print each student’s name, and not their grade, at the
end of our program, we could do the following:

.. code:: java

   for (String student : students)
   {
       System.out.println(student);
   }

We’ll use an array from time-to-time, but for the most part you should
rely on lists to store collections of values, or ordered data.

Key/Value Data: HashMaps
------------------------

Just as Python provides the dictionary structure to allow us to store
data as key/value pairs, Java also provides us a similar mechanism. Java
calls these objects hash maps (or maps, more generally), and they are
provided by the ``HashMap`` class.

Considering the gradebook example, we can improve our program using a
map, and storing students’ grades along with their names in the same
data structure. The names will be the keys, and the grades will be the
values.

Gradebook (Python Dictionary Version)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Were we to write our gradebook program above using dictionaries, we’d
come up with something like this:

.. code:: python

   def main():

       students = {}
       newStudent = " "

       print("Enter your students (or ENTER to finish):")

       # Get student names
       while (newStudent != ""):

           newStudent = input("Name: ")

           if newStudent != "":
               newGrade = float(input("Grade: "))
               students[newStudent] = newGrade

       # Print class roster
       print("\nClass roster:")
       for student in students:
           print(student + " (" + str(students[student]) + ")")

       avg = sum(students.values()) / len(students)
       print("\nAverage grade: " + str(avg))

   if __name__ == '__main__':
       main()

Gradebook (Java HashMap Version)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Let’s now turn to the Java version, using instances of the ``HashMap``
class. As with lists, in Java we must specify the types of the objects
we’ll be storing when we declare a variable or parameter to be a map.
This means specifying both key and value data types, which are allowed
to be different types for a given map.

.. code:: java

   package org.launchcode.java.demos.java4python;

   import java.util.HashMap;
   import java.util.Map;
   import java.util.Scanner;

   /**
    * Created by LaunchCode
    */
   public class GradebookHashMap {

       public static void main(String[] args) {

           HashMap<String, Double> students = new HashMap<>();
           Scanner in = new Scanner(System.in);
           String newStudent;

           System.out.println("Enter your students (or ENTER to finish):");

           // Get student names and grades
           do {

               System.out.print("Student: ");
               newStudent = in.nextLine();

               if (!newStudent.equals("")) {
                   System.out.print("Grade: ");
                   Double newGrade = in.nextDouble();
                   students.put(newStudent, newGrade);

                   // Read in the newline before looping back
                   in.nextLine();
               }

           } while(!newStudent.equals(""));

           // Print class roster
           System.out.println("\nClass roster:");
           double sum = 0.0;

           for (Map.Entry<String, Double> student : students.entrySet()) {
               System.out.println(student.getKey() + " (" + student.getValue() + ")");
               sum += student.getValue();
           }

           double avg = sum / students.size();
           System.out.println("Average grade: " + avg);
       }

   }

We can add a new item with a ``.put()`` method, specifying both key and
value: ``students.put(newStudent, newGrade)``.

And while we don’t do so in this example, we may also access ``HashMap``
elements using the ``get`` method. If we had a key/value pair of
``"jesse"/4.0`` in the ``students`` map, we could access the grade with
``Double jesseGrade = students.get("jesse")``. As with Python, variables
may be used to access elements:

.. code:: java

   String name = "jesse";
   Double jesseGrade = students.get(name);

Looping through a map is slightly more complex than it is for lists.
Let’s look at the for-each loop from this example:

.. code:: java

   for (Map.Entry<String, Double> student : students.entrySet()) {
       System.out.println(student.getKey() + " (" + student.getValue() + ")");
       sum += student.getValue();
   }

The iterator variable, ``student``, is of type
``Map.Entry<String, Double>``. The class ``Map.Entry`` is specifically
constructed to be used in this fashion, to represent key/value pairs
within HashMaps. Each ``Map.Entry`` object has a ``getKey`` method and a
``getValue`` method, which represent (surprisingly enough!), the key and
value of the map item.

If you only need to access the key of each item in a map, you can
construct a simpler loop:

.. code:: java

   for (String student : students.keySet())
   {
       System.out.println(student);
   }

A similar structure applies if you only need the values, using
``students.values()``:

.. code:: java

   for (double grade : students.values())
   {
       System.out.println(grade);
   }

HashMap Methods
~~~~~~~~~~~~~~~

Let’s collect some ``HashMap`` properties and methods. As we said about
lists, this is by no means a comprehensive list. For full details on all
properties and methods available, see the `official documentation on the
``HashMap``
class <https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html>`__.

+------------+---------------------------------+-----------------------+
| Name       | Description                     | Example               |
+============+=================================+=======================+
| ``size``   | Returns the number of items in  | ``students.size()``   |
|            | the map, as an ``int``.         |                       |
+------------+---------------------------------+-----------------------+
| ``keySet`` | Returns a collection containing | ``students.keySet()`` |
|            | all keys in the map. This       |                       |
|            | collection may be used in a     |                       |
|            | for-each loop just as lists     |                       |
|            | are, but the map *may not be    |                       |
|            | modified* within such a loop.   |                       |
+------------+---------------------------------+-----------------------+
| ``values`` | Returns a collection containing | ``students.values()`` |
|            | all values in the map. This     |                       |
|            | collection may be used in a     |                       |
|            | for-each loop just as lists     |                       |
|            | are.                            |                       |
+------------+---------------------------------+-----------------------+
| ``put``    | Add a key/value pair to a map.  | ``students.put("Mark" |
|            |                                 | , 3.5)``              |
+------------+---------------------------------+-----------------------+
| ``contains | Returns a boolean indicating    | ``students.containsKe |
| Key``      | whether or not the map contains | y("Chris")``          |
|            | a given key.                    |                       |
+------------+---------------------------------+-----------------------+
| ``contains | Returns a boolean indicating    | ``students.containsVa |
| Value``    | whether or not the map contains | lue(4.0)``            |
|            | a given value.                  |                       |
+------------+---------------------------------+-----------------------+

We have only brushed the surface of how lists and maps work, and we
leave it to you to refer to the official documentation linked below for
more details. You’ll certainly be using lists and maps in more ways than
those covered in this lesson, but with the knowledge you have now, you
should be able to use Java collections and learn new uses as you go.

References
----------

-  `Java Collections
   (docs.oracle.com) <http://docs.oracle.com/javase/8/docs/api/java/util/Collections.html>`__
-  `ArrayList Class
   (docs.oracle.com) <http://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html>`__
-  `HashMap Class
   (docs.oracle.com) <https://docs.oracle./comjavase/8/docs/api/java/util/HashMap.html>`__
-  `Arrays Tutorial
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html>`__

