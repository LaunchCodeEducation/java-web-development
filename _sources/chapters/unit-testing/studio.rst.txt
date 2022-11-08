.. _unit-testing-studio:

Studio: Unit Testing
====================

For this studio, you will be writing unit tests to help you find 
errors in provided code.

Getting Started
---------------

#. Fork the `studio repository <https://github.com/LaunchCodeEducation/junit-studio-lc101>`__.
#. In IntelliJ, check out your forked repository from Version Control.
#. Write unit tests to find the errors in ``BalancedBrackets``.
   
   a. The tests you write should guide how you revise the sourcecode. Use TDD to 
      first write tests that will work for the desired behavior of ``BalancedBrackets``.
      When your tests fail, correct the class to pass your tests.
   b. The content of your tests is up to you, but you should write at least 12 tests.

      .. admonition:: Tip

         Here's a first test to help get you started: 
         
         Assert that brackets in the correct order, ``"[]"``, return true.

         .. sourcecode:: java

            @Test
            public void onlyBracketsReturnsTrue() {
               assertTrue(BalancedBrackets.hasBalancedBrackets("[]"));
            }

.. note::

   ``BalancedBrackets`` is essentially a wrapper class for a method. And 
   because it's only method is static, we don't need to create an instance
   to test ``hasBalancedBrackets()``.
   
.. tip::

   Discuss with your fellow students and TA how the  
   class should behave. What are some examples of input, and 
   what would the desired output be for each input?

Uploading Your Work
-------------------

Push your work to save your solution in your remote repository.

Bonus Mission
-------------

The repository contains an additional branch called ``bonus_mission``
with a new class called ``BonusBinarySearch``. Create a new test file 
and write tests that pass the written description of how this class
should behave. There will be errors in the class that need to be corrected.
