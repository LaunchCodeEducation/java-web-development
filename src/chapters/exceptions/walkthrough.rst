Check the Temperature with Exceptions
=====================================

To get started with exceptions, take a look at the ``Temperature`` class we worked with when learning more about classes.

.. sourcecode:: java
   :linenos:

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
This means if we throw an exception when a value that is below absolute zero is passed to ``setFahrenheit()``, it will be a runtime exception.

Now that we know we are going to use a runtime exception, we need to answer the question: under what conditions should the exception be thrown?
In our case, that is when we attempt to set ``fahrenheit`` to a value that is below absolute zero.
Based on our knowledge of builtin Java exceptions, we know that there isn't a builtin exception that works for this, so now we need to build a custom exception.

.. sourcecode:: java
   :linenos:

   public class TemperatureException extends Exception {
	   public TemperatureException(String message){
		   super(message);
	   }
   }

We can now use this custom exception in the specific situation we need to.

.. sourcecode:: java

   public class Temperature {

       private double fahrenheit;

       public double getFahrenheit() {
           return fahrenheit;
       }

       public void setFahrenheit(double aFahrenheit) {

           double absoluteZeroFahrenheit = -459.67;

           if (aFahrenheit < absoluteZeroFahrenheit) {
               throw new TemperatureException("That temperature is too low!");
           }

           fahrenheit = aFahrenheit;
       }
   }

Now run the program!

Check Your Work
---------------

Check out the ``walkthrough-end`` branch on Github to make sure you got everything.