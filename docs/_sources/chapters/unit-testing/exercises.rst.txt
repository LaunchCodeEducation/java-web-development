Exercises: Unit Testing
=======================

Work on these exercises in the IntelliJ ``java-web-dev-exercises`` 
project. You will update your ``CarTest.java`` file by adding 
more test cases.

``testGasTankAfterDriving()``
-----------------------------

Add a test for the third TODO, "gasTankLevel is accurate after driving within tank range".

#. Your test must use the ``Car`` method ``drive()`` 

   .. sourcecode:: java

      test_car.drive(50);

#. With a value of ``50`` miles passed into ``drive()``, we expect 
   ``test_car`` to have a ``gasTankLevel`` of ``9``.

   .. sourcecode:: java

      assertEquals(9, test_car.getGasTankLevel(), .001);

``testGasTankAfterExceedingTankRange()``
----------------------------------------

Add a test for the fourth TODO, "gasTankLevel is accurate after attempting to drive past tank range".

#. You're on your own for this one. You'll need to simulate the ``Car``
   travelling farther than it's ``gasTankLevel`` allows.

``testGasOverfillException()``
------------------------------

The test for our last TODO is a little different. We are going to 
perform an action on our car object, and we are expecting the object 
to throw an error. In this case, we are going to attempt to add gas 
to our car that exceeds the gas tank size.

#. First, we'll add some text to our ``@Test`` annotation to tell JUnit
   to expect an exception. 

   .. sourcecode:: java

      //TODO: can't have more gas than tank size, expect an exception
      @Test(expected = IllegalArgumentException.class)
      public void testGasOverfillException() {

      }

   This lets JUnit know that this test should pass if an 
   ``IllegalArgumentException`` is thrown at any point during this test.

#. Update the ``Car`` class to include an ``addGas()`` method.

   .. sourcecode:: java

      public void addGas(double gas) {
        this.setGasTankLevel(gas + this.getGasTankLevel());
      }

#. Back in ``CarTest``, implement the new ``addGas()`` method and a 
   ``fail()`` scenario.

   .. sourcecode:: java

      test_car.addGas(5);
      fail("Shouldn't get here, car cannot have more gas in tank than the size of the tank");


   The ``fail()`` message will be displayed if the test fails. 
   We have to import ``fail`` into this class to use it.

#. Run the test. It should fail! In the output is an unexpected 
   exception. This test was expecting an ``IllegalArgumentException``, 
   but it got an ``AssertionError`` exception. This caused the test 
   to fail. Further down in the output log, we can see that our 
   ``fail()`` statement printed out the statement about not being 
   able to add more gas than is possible.

#. We need to refactor ``Car`` to throw an exception when too much
   gas is added to the tank. Find the ``setGasTankLevel`` method and
   modify it:

   .. sourcecode:: java

      public void setGasTankLevel(double gasTankLevel) {
         if (gasTankLevel > this.getGasTankSize()) {
            throw new IllegalArgumentException("Can't exceed tank size");
         }
        this.gasTankLevel = gasTankLevel;
      }

#. Now, run the test - it should pass!

   












