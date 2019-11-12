MVC
===

.. index:: ! design pattern, ! Model View Controller, ! MVC

So far, we have learned a lot about designing applications. What we have worked on is called a **design pattern**.
A design pattern is a set of conventions that we follow to build an application.

The **Model View Controller** pattern (MVC) is a design pattern where models, views, and controllers work together.
Data is stored in models, the user interface elements go in views, and controllers pass data from the models to the views.

.. admonition:: Example

   Let's say that we need to build an application for a bank.
   We need to keep track of how much money a customer has in their savings account.
   
   The model of the application is where the value on the customer's savings account is stored and the interface where that information is presented to the customer is the view.
   The controller of our application handles the passing of the data between our model and view so the customer can not only view their balance, but also do other necessary items like transfering money in and out of their account.

Why is this design pattern important? MVC breaks down all of the programming logic behind a user interface into three digestable components.
OOP has also taught us that the more we break down our applications into digestable components, the better. We will be able to debug an individual component as opposed to having to debug a whole application.
We will also be able to add new features to our application with ease.

Why Spring
----------

Spring is a Java framework. Using Spring, we will be able to create web applications with Java in the MVC pattern.

