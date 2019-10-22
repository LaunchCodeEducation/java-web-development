Testing in Java
===============

.. index:: ! automated testing, ! unit testing, ! JUnit, !JUnit4

You probably know by now the importance of testing your code. 
**Automated testing** in Java, like any language, ensures that 
your code works as expected, every time it runs. Tests also 
function as documentation, giving an observer instructions 
on how to properly execute your classes and methods.

This course covers **unit testing** in Java with a test runner called
**JUnit4**. Unit testing breaks down the codebase into its smallest
building blocks, individual statements and methods. 

Why We Test
^^^^^^^^^^^

Refactoring
~~~~~~~~~~~

Because they work on the most basic functionality of your code, 
unit tests safe guard against bugs introduced in refactoring.
In other words, when you write tests once, they provide a code 
lifetime's worth of benefits. 

Imagine this common workflow: You practice TDD, writing 
your tests to stipulate your class's code. You write your code
to pass your tests. Months later, a stakeholder in your project's
use requests that you refactor your code using different syntax.
The features will be the same, but the implementation changes. 
Unit tests help in this scenario in that, changes to implementation
should not require changes to outcome. Thus, if your tests continue
to pass after the refactor, you can move on, knowing you have not 
inadvertently introduced a bug.

Documentation
~~~~~~~~~~~~~

Unit tests are the most enlightened form of documentation. Again, 
because they address the most fundamental tasks of your classes,
unit tests serve as live-code use-cases. You may also have an 
external documentation directory with examples of how to run your
project, or perhaps you hve been writing comments within your code
to best communicate with your teammates about your changes. Both of
these are great choices and should be done when possible, but they 
also both require more forethought to maintain. Each time you update
your code, you may not always be also updating the documentation and 
the comments. However, with unit testing, you have a more obvious reminder
that a change has been made if a test fails after a code change.


How to Write Tests
^^^^^^^^^^^^^^^^^^

Below are some best practices to keep in mind when writing unit tests, in any language.

#. The AAAs

   The AAAs of of unit testing refers to the pattern to follow when 
   writing your unit tests. 

   #. Arrange the variables your test requires
   #. Act on the methods your test requires
   #. Assert the anticipated comparison of the expected and the actual value

