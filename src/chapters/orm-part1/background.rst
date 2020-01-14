Object-Relational Mapping
=========================

.. index:: ! Object-Relational Mapping, ! ORM, ! Java Persistence API, ! JPA, ! Data Layer

We learned that the models in MVC applications handle data and that relational databases are persistent data sources.
Now that we have these two pieces we have to connect them.
But how does a Java object acting as a model relate to a database?

**Object-Relational Mapping** or ORM is a technique for converting data between Java objects and relational databases.
In Java, a **JPA** or **Java Persistence API** handles the object-relational mapping between the classes in our model and the tables in our database.

ORM converts data between two incompatible type systems (Java and MySQL), such that each model class becomes a table in our database and each instance a row of the table.
In order to accomplish this, a JPA makes use of **data layers**. When we learned about models, we learned that :ref:`data layers <data-layer>` add abstraction between models and the data we want to store.
Models are not persistent data stores and relational databases do not shape the Java objects we will be using.
Data layers manage the passage of data between models and databases.

In Spring, our JPA for ORM is a combination of Spring Data and Hibernate.
As you run your apps, you will notice Hibernate and JPA pop up in the logs!
To run your apps, you need to connect MySQL to a Spring application. Let's do this with ``coding-events``!

.. _setup-orm-database:

Setting up a Persistent Database - Video
----------------------------------------

.. raw:: html

   <div style="text-align:center;"><iframe width="560" height="315" src="https://www.youtube.com/embed/GVOpKW3NcMk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>


Setting up a Persistent Database - Text
---------------------------------------

To get started with using a relational database as a persistent data store, we need to first go to MySQL Workbench.

In MySQL Workbench, you need to do the following:

#. Create a new schema, ``coding-events``.
#. Add a new user with a new password. Give the user all privileges to modify your new schema. 

In IntelliJ, attach MySQL to your project.

Key Takeaways
-------------

Adding the password in plain text to a file is usually bad.
While you can do it for the ``coding-events`` application, you do not want to do it in the future.

.. admonition:: Note

   To avoid this in the future, you can configure your ``application.properties`` file to use **environment variables**.
   You then hide the appropriate info by setting the environment variable's value equal to the password, for example.

Check Your Understanding
------------------------

