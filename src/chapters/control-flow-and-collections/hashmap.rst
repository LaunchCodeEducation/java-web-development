.. index:: ! HashMap, ! map

HashMap
=======

Java also provides us a structure to store data as key/value pairs. Java calls
these objects **hashmaps** (or **maps**, more generally), and they are
provided by the ``HashMap`` class.

Considering the gradebook example, we can improve our program using a
map. We'll store the students’ grades along with their names in the same
data structure. The names will be the keys, and the grades will be the
values.

As with the other collection structures, in Java we must specify the types of
the objects we’ll be storing when we declare a variable or parameter to be a
map. This means specifying both key and value data types, which are allowed
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
         Scanner input = new Scanner(System.in);
         String newStudent;

         System.out.println("Enter your students (or ENTER to finish):");

         // Get student names and grades
         do {

            System.out.print("Student: ");
            newStudent = input.nextLine();

            if (!newStudent.equals("")) {
               System.out.print("Grade: ");
               Double newGrade = input.nextDouble();
               students.put(newStudent, newGrade);

               // Read in the newline before looping back
               input.nextLine();
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


Notice how a ``HashMap`` called ``students`` is declared on line 11:

.. sourcecode:: java
   :lineno-start: 11

   HashMap<String, Double> students = new HashMap<>();

Here, ``<String, Double>`` defines the data types for this map's
``<key, value>`` pairs. Like the ``ArrayList``, when we call the ``HashMap``
constructor on the right side of the assignment, we don’t need to specify
type.

We can add a new item with a ``.put()`` method, specifying both key and
value:

.. sourcecode:: java
   :lineno-start: 26

   students.put(newStudent, newGrade);

And while we don’t do so in this example, we may also access ``HashMap``
elements using the ``get`` method. If we had a key/value pair of
``"jesse"/4.0`` in the ``students`` map, we could access the grade with:

.. sourcecode:: java

   Double jesseGrade = students.get("jesse");

Variables may be used to access elements:

.. sourcecode:: java
   :linenos:

   String name = "jesse";
   Double jesseGrade = students.get(name);

Looping through a map is slightly more complex than it is for ordered lists.
Let’s look at the ``for-each`` loop from this example:

.. sourcecode:: java
   :lineno-start: 38

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

.. sourcecode:: java
   :linenos:

   for (String student : students.keySet()) {
      System.out.println(student);
   }

A similar structure applies if you only need the values, using
``students.values()``:

.. sourcecode:: java
   :linenos:

   for (double grade : students.values()) {
      System.out.println(grade);
   }

HashMap Methods
---------------

Let’s collect some ``HashMap`` methods as we have for ``ArrayList``. As we
said about ``ArrayLists``, this is by no means a comprehensive list. For full
details on all properties and methods available, see the reference section
below for official documentation on the ``HashMap`` class.

For the purposes of this table, we'll create a map to hold our solar system's
planets and the number of moons associated with each.

.. sourcecode:: java
   :linenos:

   HashMap<String, Integer> moons = new HashMap<>();
   moons.put("Mercury", 0);
   moons.put("Venus", 0);
   moons.put("Earth", 1);
   moons.put("Mars", 2);
   moons.put("Jupiter", 79);
   moons.put("Saturn", 82);
   moons.put("Uranus", 27);
   moons.put("Neptune", 14);


.. list-table::
   :header-rows: 1

   * - Java Syntax
     - Description
     - Example
   * - ``size()``
     - Returns the number of items in the map, as an ``int``.
     - ``moons.size()`` returns ``8``
   * - ``keySet()``
     - Returns a collection containing all keys in the map. This collection may be used in a
       ``for-each`` loop just as lists are, but the map *may not be modified* within such a loop.
     - ``moons.keySet()`` returns
       ``["Earth", "Mars", "Neptune", "Jupiter", "Saturn", "Venus", "Uranus", "Mercury"]``
   * - ``values()``
     - Returns a collection containing all values in the map. This collection may be used in a
       ``for-each`` loop just as lists are.
     - ``moons.values()`` returns ``[1, 2, 14, 79, 82, 0, 27, 0]``
   * - ``put()``
     - Add a key/value pair to a map.
     - ``moons.put("Pluto", 5)`` adds ``"Pluto": 5`` to the ``moons``
   * - ``containsKey()``
     - Returns a boolean indicating whether or not the map contains a given key.
     - ``moons.containsKey("Earth")`` returns ``true``
   * - ``containsValue()``
     - Returns a boolean indicating whether or not the map contains a given value.
     - ``moons.containsValue(79)`` returns ``true``

We have only brushed the surface of how arrays, ``ArrayLists``, and maps work.
We leave it to you to refer to the official documentation linked below for more
details. You’ll certainly be using ``ArrayLists`` and maps in more ways than
those covered in this lesson, but with the knowledge you have now, you
should be able to use Java collections and learn new uses as you go.

References
----------

-  `HashMap Class
   (docs.oracle.com) <https://docs.oracle.com/en/java/javase/13/docs/api/java.base/java/util/HashMap.html>`__

Check Your Understanding
-------------------------

.. admonition:: Question

   Given our ``HashMap``,

   .. sourcecode:: java
      :linenos:

      moons = {
         "Mercury" = 0,
         "Venus" = 0,
         "Earth" = 1,
         "Mars" = 2,
         "Jupiter" = 79,
         "Saturn" = 82,
         "Uranus" = 27,
         "Neptune" = 14
      }

   What is the method to return the key names?

   #. ``Map.keys(moons);``
   #. ``moons.keys();``
   #. ``moons.keySet(moons);``
   #. ``moons.keySet();``

.. ans - ``moons.keySet();``

.. admonition:: Question

   Given our ``HashMap``,

   .. sourcecode:: java
      :linenos:

      moons = {
         "Mercury" = 0,
         "Venus" = 0,
         "Earth" = 1,
         "Mars" = 2,
         "Jupiter" = 79,
         "Saturn" = 82,
         "Uranus" = 27,
         "Neptune" = 14
      }

   What will ``moons.get("Mars");`` return?

   #. ``2``

   #. ``{Mars: 2}``

   #. ``2.0``

   #. ``"Mars"``

.. ans - ``2``
