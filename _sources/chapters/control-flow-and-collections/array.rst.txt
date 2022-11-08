Array
=====

We learned about arrays in Java in :ref:`a previous lesson <array>`, 
so let’s spend a moment comparing them to ``ArrayLists``. ``ArrayLists``  
are generally easier to use than Java's ``Array``. Let's see why this is.

Why does Java have both ``Arrays`` and ``ArrayLists``? The answer is
historical, at least in part. Java is a C-style language, and arrays are
the most basic data structure in C. Using an ``Array`` over an
``ArrayList`` might be preferred in some circumstances, primarily for
performance reasons (array operations are generally faster than ``ArrayList``
operations). Also note that *Arrays are of fixed size*. You cannot
expand or contract an ``Array`` after it is created, so you must know
exactly how many elements it will need to hold when you create it. This
fact is reason enough to use ``ArrayLists`` in most scenarios.

To illustrate ``Array`` usage, here is a version of the Gradebook program
using ``Arrays`` instead of ``ArrayLists``:

.. sourcecode:: java
   :linenos:

   package org.launchcode.java.demos.collections;

   import java.util.Scanner;

   public class ArrayGradebook {

      public static void main(String[] args) {

         // Allow for at most 30 students
         int maxStudents = 30;

         String[] students = new String[maxStudents];
         double[] grades = new double[maxStudents];
         Scanner input = new Scanner(System.in);

         String newStudent;
         int numStudents = 0;

         System.out.println("Enter your students (or ENTER to finish):");

         // Get student names
         do {
            newStudent = input.nextLine();

            if (!newStudent.equals("")) {
               students[numStudents] = newStudent;
               numStudents++;
            }

         } while(!newStudent.equals(""));

         // Get student grades
         for (int i = 0; i < numStudents; i++) {
            System.out.print("Grade for " + students[i] + ": ");
            double grade = input.nextDouble();
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

.. index:: ! bracket notation

Note that we have to decide up front how large our ``Arrays`` ``students``
and ``grades`` are going to be. Thus, this program sets an arbitrary maximum amount
of students, likely larger than any user will enter. It may seem obvious, then, 
that ``Array`` has no equivalent :ref:`add() method <arraylist-methods>`. The only 
way to access and alter an element in an ``Array`` is with **bracket notation**, 
using an explicit index. For example, gradebook defines a counter variable, ``numStudents``.
When the first student is entered by the user, the value is stored in ``newStudent``.
If the value is not the empty string, then the item in ``students`` at position 0, 
the initial value of ``numStudents`` is assigned to the ``newStudent`` value. 
The next time the ``do-while`` loop executes, the value of ``students`` at position 1
will be assigned. And so on... Because we must always access and assign ``Array`` elements using an
explicit index, our code can seem littered with ``Array``
counter variables (like our friends ``i`` and ``j``) and is more difficult to
read (not to mention more error-prone).

Like ``ArrayLists``, however, we can loop through an ``Array`` using a ``for-each``
loop as long as we don’t need to use the index of the current item. If
we only wanted to print each student’s name, and not their grade, at the
end of our program, we could do the following:

.. sourcecode:: java
   :linenos:

   for (String student : students) {
      System.out.println(student);
   }

We’ll use ``Arrays`` in Java from time-to-time, but for the most part you should
rely on ``ArrayLists`` to store collections of values, or ordered data.

References
----------

-  `Arrays Tutorial
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html>`__

Check Your Understanding
-------------------------

.. admonition:: Question

   ``Array`` size and element values cannot be changed once defined.

   #. True
   #. False

.. ans - false. array values can be changed

.. admonition:: Question

   Given the ``Array`` below, which of the following options is a valid action?

   .. sourcecode:: java 

      int[] randomNumbers = new int[5];

   #. ``randomNumbers.add(3);``
   
   #. ``randomNumbers.add("one");``

   #. ``randomNumbers[0] = "three";``

   #. ``randomNumbers[0] = 1;``

.. ans - ``randomNumbers[0] = 1;``

  