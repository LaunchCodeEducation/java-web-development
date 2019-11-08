Unit Testing and Interfaces
===========================

After all that we have learned about interfaces, you are probably wondering, *how do I write my unit tests with interfaces?*

The best practices to testing interfaces are very similar to those of :ref:`testing inheritance <testinginheritance>`. You want to focus on testing the contract that the interface is supposed to be upholding as opposed to the interface itself.

.. admonition:: Example

   We have a ``Temperature`` interface, a ``Celsius`` class, and a ``Fahrenheit`` class.

   .. sourcecode:: java
      :linenos: 

      public interface Temperature {
         double static final ABS_ZERO = -273.15;

         double convertTemp();
      }

      public class Celsius implements Temperature {

         private double currentTemp;

         @Overrides
         public double convertTemp() {
            return this.currentTemp * 9 / 5 + 32;
         }
      }

      public class Fahrenheit implements Temperature {
         
         private double currentTemp;

         @Overrides
         public double convertTemp() {
            return (this.currentTemp - 32) * 5 / 9;
         }
      }

   In this situation, we can test the contract that the interface is supposed to be upholding, but not the interface itself.
   We may choose to test that ``ABS_ZERO`` is ``-273.15`` for both ``Fahrenheit`` and ``Celsius``.
   We may also want to test that the ``convertTemp`` function works as expected, however, since ``convertTemp`` has a different method body depending on whether it is in ``Fahrenheit`` or ``Celsius``, we cannot define the as expected behavior with a test on our interface, ``Temperature``.

Check Your Understanding
------------------------

.. admonition:: Question

   True or False: You should test the interface itself.

.. ans: False
