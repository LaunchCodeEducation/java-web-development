.. index:: ! HashMap, ! map

HashMap
=======

Java also provides us a structure to store
data as key/value pairs. Java calls these objects **hashmaps** 
(or **maps**, more generally), and they are provided by the ``HashMap`` class.

Considering the gradebook example, we can improve our program using a
map. We'll store the students’ grades along with their names in the same
data structure. The names will be the keys, and the grades will be the
values.
       
As with the other collection structures, in Java we must specify the types of 
the objects we’ll be storing when we declare a variable or parameter to be a map.
This means specifying both key and value data types, which are allowed
to be different types for a given map.

.. sourcecode:: java
   :linenos:

   package org.launchcode.java.demos.collections;

   import java.util.HashMap;
   import java.util.Map;
   import java.util.Scanner;

   
   public class HashMapGradebook {

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

-  `HashMap Class
   (docs.oracle.com) <https://docs.oracle./comjavase/8/docs/api/java/util/HashMap.html>`__

