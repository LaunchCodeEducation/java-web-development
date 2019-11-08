Introduction
=============

.. index:: ! polymorphism

The third pillar of Object-Oriented Programming that we’ll
explore is polymorphism.

Polymorphism
------------

**Polymorphism** is an object-oriented mechanism that allows for objects
of different types to be used in the same way.

We’ve already encountered polymorphism made possible by inheritance when talking about :ref:`casting <casting>` with our ``Cat`` and ``HouseCat`` classes.
In that case, we stored an object of type ``HouseCat`` in its compatible type, ``Cat``.

Let's take a closer look at how polymorphism might work in our cat-centric application.

.. admonition:: Example

   Suppose we had a ``CatOwner`` class like the one below:

   .. sourcecode:: java
      :linenos:

      public class CatOwner
      {
         private Cat pet;

         public CatOwner(Cat pet) {
            this.pet = pet;
         }

         public void feedTheCat() {

            // ...code to prepare the cat's meal...

            pet.eat();
         }
      }

   The method ``feedTheCat`` uses the field ``pet``, which is of type
   ``Cat``, but since a ``HouseCat`` *is a* ``Cat`` via inheritance, it is
   perfectly acceptable to use an instance of ``HouseCat`` to fill the
   ``pet`` field.

   .. sourcecode:: java
      :linenos:

      HouseCat suki = new HouseCat("Suki", 12);
      CatOwner Annie = new CatOwner (suki);

      Annie.feedTheCat();

   Similarly, ``feedTheCat`` can accept ``Tiger`` instances as well. This
   is because the only thing that the method requires is that the input
   parameter has the methods defined within ``Cat``, and via inheritance,
   both of the subclasses satisfy this requirement.

In addition to using classes to code in a polymorphic way, we can use *interfaces*.
