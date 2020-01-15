Object-Relational Mapping
=========================

.. index:: ! Object-Relational Mapping, ! ORM, ! Java Persistence API, ! JPA, ! Data Layer

With all that we have learned about MVC applications and relational databases, we are ready to connect the two and add persistent data storage to our apps!
To do so, we need to use object-relational mapping.

**Object-Relational Mapping** or ORM is a technique for converting data between Java objects and relational databases.
ORM converts data between two incompatible type systems (Java and MySQL), such that each model class becomes a table in our database and each instance a row of the table.

In Java, a **JPA** or **Java Persistence API** handles the object-relational mapping between the classes in our model and the tables in our database.
In order to accomplish this, a JPA makes use of **data layers**.
When we learned about models, we learned that :ref:`data layers <data-layer>` add abstraction between models and the data we want to store.
Models are not persistent data stores and relational databases do not shape the Java objects we will be using.

ORM in Spring
-------------

In Spring, our JPA for ORM is a combination of Spring Data and Hibernate.
As you run your apps, you will notice Hibernate and JPA pop up in the logs!
To run your apps, you need to connect MySQL to a Spring application. Let's do this with ``coding-events``!

.. _setup-orm-database:

Setting up a Persistent Database - Video
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. raw:: html

   <div style="text-align:center;"><iframe width="560" height="315" src="https://www.youtube.com/embed/GVOpKW3NcMk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>


Setting up a Persistent Database - Text
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To get started with using a relational database with our MVC applications, we need to first go to MySQL Workbench.

In MySQL Workbench, you need to do the following:

#. Create a new schema, ``coding-events``.
#. Add a new user with a new password. Give the user all privileges to modify your new schema. 

In IntelliJ, attach MySQL to your project in ``application.properties``.

.. sourcecode:: guess

   # Database connection settings
   spring.datasource.url=jdbc:mysql://localhost:3306/coding_events
   spring.datasource.username=user
   spring.datasource.password=greatpassword

Set the value of ``username`` and ``password`` to the username and password you set up in MySQL Workbench.

In the ``dependencies`` of ``build.gradle``, add MySQL and the Spring Data JPA, like so:

.. sourcecode:: guess

   implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
   implementation 'mysql:mysql-connector-java'

Once you have taken these steps, you are ready to set up the appropriate models and controllers for the application!

Key Takeaways
^^^^^^^^^^^^^

Before we can get into the ins and outs of using ORM, we need to make sure that our application has a corresponding database and that our application is ready to connect to MySQL.
We can start to do this by creating new schemas and setting user privileges in MySQL Workbench.
We also *must* make sure that the Spring application has the correct dependencies and the username and password to access the schema.

If we do not do these steps, then our application will not be able to use a persistent data source.

As Chris noted in our video, while we can simply set the value of ``spring.datasource.username`` and ``spring.datasource.password`` to the value of the username and password, this is not best practice.
We regularly commit our code to Github, meaning anyone who reads the code in our repository can see the username and password.
While you can do it for the ``coding-events`` application, you do not want to do it in the future.

To avoid this in the future, you can configure your ``application.properties`` file to use **environment variables**.
You then hide the appropriate info by setting the environment variable's value equal to the password, for example.

We have written an `article <https://education.launchcode.org/gis-devops/configurations/02-environment-variables-intellij/index.html>`_ on how to configure your environment variables to keep the username and password to your database safe and secure.

Check Your Understanding
------------------------

.. admonition:: Question

   True or false: writing usernames and passwords in plain text in a file is a GREAT idea!

.. ans: False

.. admonition:: Question

   True or false: an ORM converts data between Java objects and relational databases.

.. ans: True

.. admonition:: Question

   True or false: We need Hibernate AND Spring Data to successfully use ORM.

.. ans: True
