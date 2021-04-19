.. _unit-testing-exercise-solutions:

Exercise Solutions: Unit Testing
================================

.. _unit-testing-exercise-solutions1:

``testGasTankAfterDriving()``
-----------------------------

Add a test for the third TODO, "gasTankLevel is accurate after driving within tank range".

After following the steps, your test should look like the following:

.. sourcecode:: java

   @Test
   public void testGasTankAfterDriving() {
      test_car.drive(50);
      assertEquals(9, test_car.getGasTankLevel(),.001);
   }

:ref:`Back to the exercises <unit-testing-exercises>`

.. _unit-testing-exercise-solutions2:

``testGasTankAfterExceedingTankRange()``
----------------------------------------

Add a test for the fourth TODO, "gasTankLevel is accurate after attempting to drive past tank range".

.. sourcecode:: java

   @Test
   public void testGasTankAfterExceedingTankRange() {
      test_car.drive(501);
      assertEquals(test_car.getGasTankLevel(), 0, .001);
   }

:ref:`Back to the exercises <unit-testing-exercises>`

.. _unit-testing-exercise-solutions3:

``testGasOverfillException()``
------------------------------

The test for our last TODO is a little different. We are going to 
perform an action on our car object, and we are expecting the object 
to throw an error. In this case, we are going to attempt to add gas 
to our car that exceeds the gas tank size.

After following the steps, your test should look like the following:

.. sourcecode:: java

   @Test(expected = IllegalArgumentException.class)
   public void testGasOverfillException() {
      test_car.addGas(5);
      fail("Shouldn't get here, car cannot have more gas in tank than the size of the tank");
   }

:ref:`Back to the exercises <unit-testing-exercises>`
