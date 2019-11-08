.. _testinginheritance:

Testing Inheritance
===================

Not sure you get the whole inheritance idea? Still not sure which fields and methods get inherited and 
which are overridden? Looking to *test* your understanding? (wink)

Knowing what we know now about :ref:`unit-testing` and :ref:`inheritance`, we can test that our 
subclasses extend their base classes.

We can add a ``test`` folder to our ``inheritance`` package and write some code to ensure that 
``HouseCat`` inherits what we expect it to.

.. sourcecode:: java
   :linenos:

   @Test
   public void inheritsSuperInFirstConstructor() {
      HouseCat keyboardCat = new HouseCat("Keyboard Cat", 7);
      assertEquals(7, keyboardCat.getWeight(), .001);
   }

Here, we're testing that one of our ``HouseCat`` constructors will call the ``Cat`` constructor
and appropriately assign the ``HouseCat`` object's ``weight`` property. Remember, we don't need
to write unit tests for getters or setters unless they do something extra in addition to getting
or setting. The purpose of this test, though, is less to test getting ``keyboardCat.weight`` 
and more to validate that the subclass constructor has inherited the base class constructor.

It's a good practice to test your subclasses to verify the items that they inherit or override.

Check Your Understanding
------------------------

.. admonition:: Question

   
   Fill in the blank to test that the default constructor of ``Cat`` is called when the second 
   constructor on ``HouseCat`` is used?

   Second ``HouseCat`` constructor:

   .. sourcecode:: java
      :lineno-start: 14

      public HouseCat(String aName) {
        name = aName;
      }

   .. sourcecode:: java
      :linenos:

      @Test
      public void inheritsDefaultCatInSecondConstructor() {
         HouseCat keyboardCat = new HouseCat("Keyboard Cat");
         <insert assertion method here>
      }

   a. ``assertEquals(13, keyboardCat.getWeight());``

   b. ``assertNotNull(keyboardCat.getWeight());``

   c. ``assertEquals(13, keyboardCat.getWeight(), .001);``

   d. ``assertNotNull(keyboardCat.weight);``

.. ans c, ``assertEquals(13, keyboardCat.getWeight(), .001);``

.. admonition:: Question

   What additional assert method can we add to this test to properly verify that ``HouseCat``
   inherits ``eat()``?

   .. sourcecode:: java
      :linenos:

      @Test
      public void isNotInitiallyTired() {
         HouseCat keyboardCat = new HouseCat("Keyboard Cat");
         assertFalse(keyboardCat.isHungry());
         assertFalse(keyboardCat.isTired());
         keyboardCat.eat();
      }

   a. ``assertFalse(keyboardCat.isTired());``

   b. ``assertTrue(keyboardCat.isTired());``

   c. ``assertTrue(keyboardCat.isHungry());``

   d. ``assertFalse(keyboardCat.tired);``

.. ans b, ``assertTrue(keyboardCat.isTired());``

