Check the Temperature with Exceptions
=====================================

To get started with exceptions, fork and clone this `repository <https://github.com/LaunchCodeEducation/java-web-dev-exceptions>`__ to your machine so you can code along.
Inside the ``Temperature`` package, take a look at the ``Temperature`` class.
We worked with this exact class when learning more about :ref:`classes <temperature-class>`.

.. sourcecode:: java
   :lineno-start: 3

   public class Temperature {

       private double fahrenheit;

       public double getFahrenheit() {
           return fahrenheit;
       }

       public void setFahrenheit(double aFahrenheit) {

           double absoluteZeroFahrenheit = -459.67;

           if (aFahrenheit < absoluteZeroFahrenheit) {
               System.out.println("Value is below absolute zero");
           }

           fahrenheit = aFahrenheit;
       }
   }

Instead of simply printing out a warning that the temperature is below absolute zero, let's use exceptions to handle this case.

Before coding with exceptions, first think about what the exception needs to handle.
In the case of our ``Temperature`` class, we need to throw an exception if the program attempts to set the value of ``fahrenheit`` to a temperature that is below absolute zero.
The first question we need to ask about this exception is: when will it be thrown?
Exceptions in Java can either be checked or unchecked depending on if the exception is a compile-time exception or a runtime exception.
In the context of a larger program, ``setFahrenheit()`` is only called with a value that is given by a user.
This means if we throw an exception when a value that is below absolute zero is passed to ``setFahrenheit()``, it will be a runtime or unchecked exception.

Now that we know we are going to use a runtime exception, we need to answer the question: under what conditions should the exception be thrown?
In our case, that is when we attempt to set ``fahrenheit`` to a value that is below -459.67.
Based on our knowledge of builtin Java exceptions, we know that there isn't a builtin exception that works for this, so now we need to build a custom exception.

Turn your attention to the ``TemperatureException`` class. Here is where we need to start coding.
First, all custom exceptions must inherit from the ``Exception`` class.

.. sourcecode:: java
   :lineno-start: 3

   public class TemperatureException extends Exception {
      // Write code here!
   }

With the relationship between the two classes set up, we now need to add a constructor. In this case, that is all we need to add.
We do not want to call the ``Exception`` class directly, so we will use ``TemperatureException`` to access its properties.
The constructor will only have to deal with a ``message`` parameter.

.. sourcecode:: java
   :lineno-start: 4

   public TemperatureException(String message){
        super(message);
    }

We now have a custom exception ready for use!
Back in the ``Temperature`` class, we need to use this exception to prevent the temperature from being set to a value that is below absolute zero.
You may be tempted to just throw the exception if the value is below absolute zero, like so:

.. sourcecode:: java
   :lineno-start: 15

   if (aFahrenheit < absoluteZeroFahrenheit) {
      throw new TemperatureException("That temperature is too low!");
   }

However, if you do this, you will get an error in IntelliJ. You get this error because, in Java, we must handle every exception that is thrown.
We need to encase our exception in a ``try/catch`` block. We want to *try* to throw the exception and if we *catch* the error, we want to print the stack trace.

.. sourcecode:: java
   :lineno-start: 15

   if (aFahrenheit < absoluteZeroFahrenheit) {
      try {
            throw new TemperatureException("That temperature is too low!");
      } catch (TemperatureException e) {
            e.printStackTrace();
      }
   }


Now run the program and try to enter a value below absolute zero!

Check Your Work
---------------

Check out the ``end-of-walkthrough`` branch on Github to make sure your code is correct.