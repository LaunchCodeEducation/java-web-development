Design Patterns, MVC, and Spring, Oh My!
========================================

.. index:: ! design pattern, ! Model-View-Controller, ! MVC, ! model, ! view, ! controller

So far, we have been designing our applications by diagrammming classes, drawing connections, and adding in interfaces.
This practice benefits us because we can start seeing issues *before* we start coding.
Many software developers start their applications with this process.
But before we start diagramming our ``Cat`` class and our ``HouseCat`` class, we decide on the template for our design that we want to use.
These design templates that are abstract solutions to common software architecture problems are called **design patterns**.
Design patterns provide a set of conventions that we follow to build an application.

**Model-View-Controller** (MVC) is a design pattern where the programming logic behind the application is broken down into 3 components: models, views, and controllers.
A **model** handles the data and business logic of the application. A **view** handles the user interface elements.
A **controller** passes information from the models to the views. Controllers are the "traffic cops" of the application, capable of passing data back and forth to the browser in MVC web applications. This process will be covered in depth later on in this chapter.

.. TODO: Add figure showing the relationship between models, views, and controllers.

Because MVC breaks down all of the programming logic of an application into three digestable components, we can use this particular design pattern to make extensible applications.
We also use MVC because it separates the components of the programs that the user interacts with from the underlying business logic.

.. index:: ! Spring

Spring
------

**Spring** is a Java framework. We will be using Spring Boot, an extension of Spring MVC to build Java based web applications with the MVC design pattern.

