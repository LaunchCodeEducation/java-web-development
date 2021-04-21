.. _interfaces-and-polymorphism-exercise-solutions:

Exercise Solutions: Interfaces and Polymorphism
===============================================

.. _interfaces-and-polymorphism-exercise-solutions1:

Sorting Flavors by Name
-----------------------

Create a Sorting Class
^^^^^^^^^^^^^^^^^^^^^^

#. Create a new class called ``FlavorComparator`` and have it implement the
   ``Comparator`` interface:

   .. sourcecode:: java

      public class FlavorComparator implements Comparator<Flavor>

#. Always returning ``0`` results in no sorting, so replace line 8 with:

   .. sourcecode:: java

      return o1.getName().compareTo(o2.getName());

   This returns an integer (negative, positive, or zero) depending on
   whether ``Flavor`` object ``o1`` or ``o2`` comes first, alphabetically.

.. sourcecode:: java

   public class FlavorComparator implements Comparator<Flavor> {
      @Override
      public int compare(Flavor flavor1, Flavor flavor2) {
         return flavor1.getName().compareTo(flavor2.getName());
      }
   }

:ref:`Back to the exercises <interfaces-and-polymorphism-exercises>`

.. _interfaces-and-polymorphism-exercise-solutions3:

Sorting Cones by Cost
----------------------

Now let's sort our ``cones`` list by cost, from least expensive to most
expensive.

#. Create the new class ``ConeComparator``.
#. Follow the example above to implement the ``Comparator`` interface and
   evaluate ``Cone`` objects by cost.
#. In ``Main``, sort the ``cones`` list, then print the elements to the screen
   to verify the results.

   .. sourcecode:: bash

      Before:           After:

      Waffle: $1.25        Bowl: $0.05
      Sugar: $0.75         Wafer: $0.50
      Wafer: $0.50         Sugar: $0.75
      Bowl: $0.05          Waffle: $1.25

.. sourcecode:: java

   public class ConeComparator implements Comparator<Cone> {
      @Override
      public int compare(Cone cone1, Cone cone2) {
         if (cone1.getCost() - cone2.getCost() < 0){
            return -1;
         } else if (cone1.getCost() - cone2.getCost() > 0) {
            return 1;
         } else {
            return 0;
         }
      }
   }

:ref:`Back to the exercises <interfaces-and-polymorphism-exercises>`