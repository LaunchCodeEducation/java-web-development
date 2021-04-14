.. _data-types-exercise-solutions:

Exercise Solutions: Data Types
==============================

Part 2: Exercises
-----------------

.. _data-types-exercise-solutions2a:

#. **Input/output**: Write a new "Hello, World" program to prompt the
   user for their name and greet them by name. After the given steps, you should have a ``HelloWorld`` class that looks like the following:

   .. sourcecode:: java
      :linenos:

      package exercises.lsn1datatypes;
      import java.util.Scanner;

      public class HelloWorld {
         public static void main(String[] args) {
            Scanner input = new Scanner(System.in);
            System.out.println("Hello, what is your name:");

            String name = input.nextLine();
            System.out.println("Hello " + name);
         }
      }

   :ref:`Back to the exercises <data-types-exercises>`

.. _data-types-exercise-solutions2b:

3. **Numeric types**: Write a program that asks a user for the number of miles they have driven and the amount of gas they’ve consumed (in gallons), and print their miles-per-gallon.

   .. sourcecode:: java
      :linenos:

      package exercises.lsn1datatypes;
      import java.util.Scanner;

      public class Miles {
         public static void main(String[] args) {
            Scanner input = new Scanner(System.in);

            System.out.println("How many miles have you driven?");
            Double numMiles = input.nextDouble();

            System.out.println("How much gas did you use? In gallons.");
            Double numGallons = input.nextDouble();

            Double mpg = numMiles / numGallons;
            System.out.println("You are running on " + mpg + " mpg.");
         }
      }

   :ref:`Back to the exercises <data-types-exercises>`

.. _data-types-exercise-solutions2c:

5. **Strings**: Extend the previous exercise. Assume the user enters a word that is in the sentence. Print out its index within the string and its length. Next, remove the word from the string and print the sentence again to confirm your code. Remember that strings are *immutable*, so you will need to reassign the old sentence variable or create a new one to store the updated phrase.

   .. sourcecode:: java
      :linenos: 

      Integer index = firstSentence.indexOf(searchTerm);
      Integer length = searchTerm.length();
      System.out.println("Your search term first appears at index " + index + ". Your term is " + length + " characters long.");
      String modifiedSentence = firstSentence.replace(searchTerm, "");
      System.out.println(modifiedSentence);

   :ref:`Back to the exercises <data-types-exercises>`