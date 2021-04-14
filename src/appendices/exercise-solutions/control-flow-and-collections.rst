.. _control-flow-and-collections-exercise-solutions:

Exercise Solutions: Control Flow and Collections
================================================

Array Practice
--------------

.. _control-flow-and-collections-exercise-solutions1a:

#. Create and initialize an array with the following values in a single line:
   ``1, 1, 2, 3, 5, 8``.

   .. sourcecode:: java

      int[] integerArray = {1, 1, 2, 3, 5, 8};

   :ref:`Back to the exercises <control-flow-and-collections-exercises>`

.. _control-flow-and-collections-exercise-solutions1b:

3. For this exercise, use the string ``I would not, could not, in a box. I
   would not, could not with a fox. I will not eat them in a house. I will not
   eat them with a mouse.`` Use the ``split`` method to divide the string at
   each space and store the individual words in an array. If you need to review
   the method syntax, look back at the :ref:`String methods <string-methods>`
   table.

   .. sourcecode:: java

      String phrase = "I would not, could not, in a box. I would not, could not with a fox. I will not eat them in a house. I will not eat them with a mouse.";
      String[] words = phrase.split(" ");
      System.out.println(Arrays.toString(words));

   :ref:`Back to the exercises <control-flow-and-collections-exercises>`

.. _control-flow-and-collections-exercise-solutions1c:

5. Repeat steps 3 and 4, but change the delimiter to split the string into
   separate sentences.

   .. sourcecode:: java

      String[] sentences = phrase.split("\\.");
      System.out.println(Arrays.toString(sentences));

   :ref:`Back to the exercises <control-flow-and-collections-exercises>`

ArrayList Practice
------------------

.. _control-flow-and-collections-exercise-solutions2a:

#. Write a static method to find the sum of all the even numbers in an
   ArrayList. Within ``main``, create a list with at least 10 integers and call
   your method on the list.

   .. sourcecode:: java
      :linenos:

      public static int sumEven(ArrayList<Integer> arr) {
         int total = 0;
         for (int integer : arr) {
            if (integer % 2 == 0) {
               total += integer;
            }
         }
         return total;
      }

   :ref:`Back to the exercises <control-flow-and-collections-exercises>`

.. _control-flow-and-collections-exercise-solutions2b:

3. Modify your code to prompt the user to enter the word length for the search.

   .. sourcecode:: java

      System.out.println("Enter a word length: ");
      int numChars = input.nextInt();

   :ref:`Back to the exercises <control-flow-and-collections-exercises>`

HashMap Practice
----------------

.. _control-flow-and-collections-exercise-solutions3:

Make a program similar to ``GradebookHashMap`` that does the following:

#. It takes in student names and ID numbers (as integers) instead of names and
   grades.
#. The keys should be the IDs and the values should be the names.
#. Modify the roster printing code accordingly.

.. sourcecode:: java
   :linenos:

   do {
      System.out.print("Student: ");
      newStudent = input.nextLine();

      if (!newStudent.equals("")) {
         System.out.print("ID: ");
         Integer newID = input.nextInt();
         classRoster.put(newID, newStudent);

         input.nextLine();
      }
   } while(!newStudent.equals(""));

   input.close();

   System.out.println("\nClass roster:");

   for (Map.Entry<Integer, String> student : classRoster.entrySet()) {
      System.out.println(student.getValue() + "'s ID: " + student.getKey());
   }

   System.out.println("Number of students in roster: " + classRoster.size());

:ref:`Back to the exercises <control-flow-and-collections-exercises>`
