Conditionals
============

Control flow statements in Java --- conditionals and loops --- are very
straightforward.

.. index:: ! if statement

``if`` Statements
-----------------

Let’s consider an **if statement** with no ``else`` clause.

In Java this pattern is simply written as:

.. sourcecode:: java
   :linenos:

   if (condition) {
      statement1
      statement2
      ...
   }

You can see that in Java the curly braces define a block.
Parentheses around the condition are required.

.. index:: ! else clause

``if else``
-----------

Adding an **else clause**, we have:

.. sourcecode:: java
   :linenos:

   if (condition) {
      statement1
      statement2
      ...
   } else {
      statement1
      statement2
      ...
   }

.. index:: ! else if

``else if``
-----------

An **else if** construction in Java:

.. sourcecode:: java
   :linenos:

    import java.util.Scanner;

    public class ElseIf {
        public static void main(String args[]) {
            Scanner in = new Scanner(System.in);
            System.out.println("Enter a grade: ");
            int grade = in.nextInt();
            if (grade < 60) {
                System.out.println('F');
            } else if (grade < 70) {
                System.out.println('D');
            } else if (grade < 80) {
                System.out.println('C');
            } else if (grade < 90) {
                System.out.println('B');
            } else {
                System.out.println('A');
            }
        }
    }


.. index:: ! switch, ! case, ! break

.. _switch-statements:

``switch`` Statements
---------------------

Java also supports a **switch** statement that acts something like an
``else if`` statement under certain conditions, called **cases**. The
``switch`` statement is  not used very often, and we generally recommend you
avoid using it. It is not as powerful as the ``else if`` model because the
``switch`` variable can only be compared for equality with a very small class
of types.

Here is a quick example of a ``switch`` statement:

.. sourcecode:: java
   :linenos:

   import java.util.Scanner;

   public class DayPrinter {
      public static void main(String[] args) {
         Scanner in = new Scanner(System.in);
         System.out.println("Enter an integer: ");
         int dayNum = in.nextInt();

         String day;
         switch (dayNum) {
            case 0:
               day = "Sunday";
               break;
            case 1:
               day = "Monday";
               break;
            case 2:
               day = "Tuesday";
               break;
            case 3:
               day = "Wednesday";
               break;
            case 4:
               day = "Thursday";
               break;
            case 5:
               day = "Friday";
               break;
            case 6:
               day = "Saturday";
               break;
            default:
               // in this example, this block runs if none of the above blocks match
               day = "Int does not correspond to a day of the week";
         }
         System.out.println(day);
      }
   }

In the example above, here's the output if a user enters the number ``4``.

.. sourcecode:: bash

   Enter an integer: 4
   Thursday

And the output if that user enters ``10``? Below:

.. sourcecode:: java

   Enter an integer: 10
   Int does not correspond to a day of the week


Here's how the above example looks using the ``else if`` construction:

.. sourcecode:: java
   :linenos:

   import java.util.Scanner;

   public class DayPrinter {
      public static void main(String[] args) {
         Scanner in = new Scanner(System.in);
         System.out.println("Enter an integer: ");
         int dayNum = in.nextInt();

         String day;
         if (dayNum == 0) {
           day = "Sunday";
         } else if (dayNum == 1){
           day = "Monday";
         } else if (dayNum == 2){
           day = "Tuesday";
         } else if (dayNum == 3){
           day = "Wednesday";
         } else if (dayNum == 4){
           day = "Thursday";
         } else if (dayNum == 5){
           day = "Friday";
         } else if (dayNum == 6){
          day = "Saturday";
         } else {
          day = "Int does not correspond to a day of the week";
         }
         System.out.println(day);
      }
   }

.. index:: ! fallthrough

Fallthrough
^^^^^^^^^^^

Additionally, if **break statements** are omitted from the individual
cases on accident, a behavior known as
`fallthrough <https://en.wikipedia.org/wiki/Switch_statement#Fallthrough>`__
is carried out. **Fallthrough** can be quite unintuitive, and is only
desirable in very specific circumstances. We will discuss ``break``
statements in more detail in the loop section below. For now, just
know that when used in a ``switch`` block, they terminate the ``switch``
statement they are in, so the flow of control in your program moves to
the next statement after the switch block.

Here’s a quick example of how fallthrough works:

.. sourcecode:: java
   :linenos:

   import java.util.Scanner;

   public class DayPrinter {
      public static void main(String[] args) {

         System.out.println("Enter an integer: ");
         Scanner in = new Scanner(System.in);
         int dayNum = in.nextInt();

         String day;
         switch (dayNum) {
            case 0:
               day = "Sunday";
            case 1:
               day = "Monday";
            case 2:
               day = "Tuesday";
            case 3:
               day = "Wednesday";
            case 4:
               day = "Thursday";
            case 5:
               day = "Friday";
            case 6:
               day = "Saturday";
            default:
               // in this example, this block runs even if one of the above blocks match
               day = "Int does not correspond to a day of the week";
         }
         System.out.println(day);
      }
   }

This time, without the ``break`` statements in each ``case``, if the
user enters ``4``, they will see the default output:

.. sourcecode:: bash

   Enter an integer: 4
   Int does not correspond to a day of the week


This is because after the ``switch`` statement matches the
``case`` for ``4`` and assigns the value ``Thursday`` to the variable
``day``, it proceeds to execute every statement in every case that
follows, all the way through the ``default`` case. So the ``String``
that ends up being printed will reflect the last executed statement in
the ``switch`` block.

Along similar lines, consider this variation on the code block above:

.. sourcecode:: java
   :linenos:

   import java.util.Scanner;

   public class DayPrinter {
      public static void main(String[] args) {

         System.out.println("Enter an integer: ");
         Scanner in = new Scanner(System.in);
         int dayNum = in.nextInt();

         String day;
         switch (dayNum) {
            case 0:
               day = "Sunday";
            case 1:
               day = "Monday";
            case 2:
               day = "Tuesday";
            case 3:
               day = "Wednesday";
            case 4:
               day = "Thursday";
            case 5:
               day = "Friday";
            case 6:
               day = "Saturday";
               break;
            default:
               day = "Int does not correspond to a day of the week";
         }
         System.out.println(day);
      }
   }


Here, we have a ``break`` statement in ``case 6`` after ``day = "Saturday";``.
If the user enters ``4``, the execution will fallthrough until it reaches that
``break`` statement and ``Saturday`` is printed instead of ``Thursday``.
The output:

.. sourcecode:: bash

   Enter an integer: 4
   Saturday



References
----------

-  `The if-then and if-then-else Statements
   (docs.oracle.com) <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/if.html>`__
-  `The switch Statement
   (docs.oracle.com) <http://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html>`__

Check Your Understanding
-------------------------

.. admonition:: Question

   When does fallthrough occur in Java?

   #. Omitting an ``else`` clause from a conditional.
   #. Omitting an ``else`` clause from switch statement.
   #. Omitting a ``default`` case from a ``switch`` statement.
   #. Omitting a ``break`` line from a ``switch`` statement.

.. ans: Omitting a break line from a switch statement.

.. admonition:: Question

   .. sourcecode:: java
      :linenos:

      import java.util.Scanner;

      public class QuizQuestion {
         public static void main(String[] args) {

            System.out.println("Are you a space cadet? yes or no");
            Scanner in = new Scanner(System.in);
            String response = in.next();

            switch (response) {
               case "yes":
                  System.out.println("Greetings cadet.");
               case "no":
                  System.out.println("Greetings normie.");
               default:
                  System.out.println("Are you an alien?");
            }
         }
      }

   Given the code above, what prints if the user enters ``no`` after the prompt?

   #. 
   
      .. sourcecode:: bash
      
         Greetings cadet.
   #. 
   
      .. sourcecode:: bash
      
         Greetings normie.

   #. .. sourcecode:: bash
   
         Greetings normie.
         Are you an alien?
   #. 
   
      .. sourcecode:: bash
      
         Greetings cadet.
         Greetings normie.

.. ans:  Greetings normie.
         Are you an alien?

