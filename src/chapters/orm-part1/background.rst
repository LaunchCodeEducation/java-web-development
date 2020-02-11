Object-Relational Mapping
=========================

.. index:: ! Object-Relational Mapping, ! ORM, ! Java Persistence API, ! JPA, ! Data Layer, ! object-relational mapper

With all that we have learned about MVC applications and relational databases, we are ready to connect the two and add persistent data storage to our apps!
To do so, we need to use *object-relational mapping*.

**Object-Relational Mapping** or **ORM** is a technique for converting data between Java objects and relational databases.
ORM converts data between two incompatible type systems (Java and MySQL), such that each model class becomes a table in our database and each instance a row of the table.

.. admonition:: Example

   Let's say we have a Java class called ``ContactInfo``. ``ContactInfo`` has three fields: an integer ``id``, a string ``name``, and a string ``email``.
   Now we want to store this information in a MySQL database.
   We can use ORM so that the database of our application has a table to contain all objects instantiated from the ``ContactInfo`` class.
   The table called ``contactinfo`` has three columns: an integer ``id``, a varchar ``name``, and a varchar ``email``.

   Now, let's instantiate a Java object:

   .. sourcecode:: java

      public frank = new ContactInfo(3,"Frank","frank@email.com"); 

   Having properly set up our application, we can add Frank's info to our ``contactinfo`` table.
   While we will write the code to add Frank's info to our database in Java, the frameworks and APIs that make ORM happen will run the following MySQL query for us.

   .. sourcecode:: mysql

      INSERT INTO contactinfo (id,name,email)
      VALUES (3,"Frank","frank@email.com");
   
   Now Frank's info is safely stored in our MySQL database in the ``contactinfo`` table!

At the most basic level, we need two components to make ORM work in our Java applications: an API and an object-relational mapper.
The API will set the standards by which the **object-relational mapper** will convert between Java and MySQL.
In the example above, the API reads through our Java code and designates a class that will be turned into a table.
The mapper will then read through the class and create the following MySQL query to make the ``contactinfo`` table.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE contactinfo (
      INT id,
      VARCHAR(255) name,
      VARCHAR(255) email
   );

In Java, this API is called a **JPA** or **Java Persistence API**.
JPAs makes use of **data layers**.
When we learned about models, we learned that :ref:`data layers <data-layer>` add abstraction between models and the data we want to store.
Models are NOT persistent data stores and relational databases do NOT shape the Java objects we will be using.
We want to make sure that the two remain separate.

.. index:: ! Spring Data JPA, ! Hibernate

ORM in Spring
-------------

In Spring, our JPA is called the **Spring Data JPA**. If you look up JPA on the internet, you will find many different examples!
While JPAs follow the same set of standards, different frameworks have different JPAs that work within their specific framework.
The object-relational mapper we will be using with the Spring Data JPA is **Hibernate**. 
As you run your apps, you will notice Hibernate and JPA pop up in the logs!
To run your apps, you need to connect MySQL to a Spring application. Let's do this with ``coding-events``!

.. _setup-orm-database:

Setting up a Persistent Database - Video
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following video explains how we can add a MySQL database to our ``coding-events`` application. 
The accompanying text is a quick rundown of what happens in the video. To get started, create a branch off of your `enums <https://github.com/LaunchCodeEducation/coding-events/tree/enums>`_ branch.

.. youtube::
   :video_id: GVOpKW3NcMk
   :gh_path: LaunchCodeEducation/coding-events/db-config


Setting up a Persistent Database - Text
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To get started with using a relational database with our MVC applications, we need to first go to MySQL Workbench.

In MySQL Workbench, you need to do the following:

#. Create a new schema, ``coding-events``.

   .. admonition:: Note

      In the video, Chris names his schema ``coding_events``. Either name works just fine, as long as you are 
      consistent within your own application.
   
   
#. Add a new user with a new password. Give the user all privileges to modify your new schema. 


In IntelliJ, attach MySQL to your project in ``application.properties``.

.. sourcecode:: guess

   # Database connection settings
   spring.datasource.url=jdbc:mysql://localhost:3306/coding-events
   spring.datasource.username=user
   spring.datasource.password=greatpassword

   # Specify the DBMS
   spring.jpa.database = MYSQL

   # Show or not log for each sql query
   spring.jpa.show-sql = false

   # Hibernate ddl auto (create, create-drop, update)
   spring.jpa.hibernate.ddl-auto = update

   # Use spring.jpa.properties.* for Hibernate native properties (the prefix is
   # stripped before adding them to the entity manager)
   spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL8Dialect

Set the value of ``username`` and ``password`` to the username and password you set up in MySQL Workbench.

In the ``dependencies`` of ``build.gradle``, add MySQL and the Spring Data JPA, like so:

.. sourcecode:: groovy

   implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
   implementation 'mysql:mysql-connector-java'

Once you have taken these steps, you are ready to set up the appropriate models and controllers for the application!

.. index:: ! environment variables

Key Takeaways
^^^^^^^^^^^^^

Before we can get into the ins and outs of using ORM, we need to make sure that our application has a corresponding database and that our application is ready to connect to MySQL.
We can start to do this by creating new schemas and setting user privileges in MySQL Workbench.
We also *must* make sure that the Spring application has the correct dependencies, username, and password to access the schema.

If we do not do these steps, then our application will not be able to use a persistent data source.

As Chris noted in our video, while we can simply set the value of ``spring.datasource.username`` and ``spring.datasource.password`` to the value of the username and password, this is NOT best practice.
We regularly commit our code to Github, meaning anyone who reads the code in our repository can see the username and password.
While you can do it for the applications in this class, you do not want to do it in the future.

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
