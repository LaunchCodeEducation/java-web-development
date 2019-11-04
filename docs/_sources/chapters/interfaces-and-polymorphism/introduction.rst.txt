Introduction
============

The third **Pillar of Object-Oriented Programming** that we’ll
explore is **polymorphism**.

Polymorphism
------------


**polymorphism**: An object-oriented mechanism that allows for objects
of different types to be used in the same way.


We’ve already encountered polymorphism made possible by inheritance.

Suppose we had a ``CatOwner`` like below.

.. code:: java

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

.. code:: java

   HouseCat suki = new HouseCat("Suki", 12);
   CatOwner Annie = new CatOwner (suki);

   Annie.feedTheCat();

Similarly, ``feedTheCat`` can accept ``Tiger`` instances as well. This
is because the only thing that the method requires is that the input
parameter has the methods defined within ``Cat``, and via inheritance,
both of the subclasses satisfy this requirement. This is an example of
polymorphism.

There’s one more object-oriented mechanism that empowers us to code in a
polymorphic way: the interface.
