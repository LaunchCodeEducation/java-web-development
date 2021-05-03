.. _inheritance-exercise-solutions:

Exercise Solutions: Inheritance
===============================

After working through the exercises, your ``Computer``, ``Laptop``, and ``Smartphone`` classes should look similar to the following examples.

The ``Computer`` class:

.. sourcecode:: java
   :linenos:

   public class Computer extends AbstractEntity{
      // computer is my parent class

      private int ram;
      private int storage;
      private boolean hasKeyboard;

      public Computer(int storage, int ram, boolean hasKeyboard) {
         super();
         this.ram = ram;
         this.storage = storage;
         this.hasKeyboard = hasKeyboard;
      }

      public void increaseRAM (int n) {
         this.ram = this.ram + n;
      }

      public void increaseStorage (int x) {
         this.storage = this.storage + x;
      }
   }

The ``Laptop`` class:

.. sourcecode:: java
   :linenos:

   public class Laptop extends Computer {

      private double weight; // laptop weight in pounds.

      public Laptop(int storage, int ram, boolean hasKeyboard, double weight) {
         super(storage, ram, hasKeyboard);
         this.weight = weight;
      }

      public boolean isClunky() {
         if (weight > 5.0) {
            return true;
         }
         else {
            return false;
         }
      }
   }  

The ``SmartPhone`` class:

.. sourcecode:: java
   :linenos:

   public class SmartPhone extends Computer {

      private int numberOfSelfies;

      public SmartPhone(int storage, int ram, boolean hasKeyboard, int numberOfSelfies) {
         super(storage, ram, hasKeyboard);
         this.numberOfSelfies = numberOfSelfies;
      }

      public void takeSelfie() {
         this.numberOfSelfies = this.numberOfSelfies + 1;
      }

      public int getNumberOfSelfies() {
         return this.numberOfSelfies;
      }
   }

:ref:`Back to the exercises <inheritance-exercises>`