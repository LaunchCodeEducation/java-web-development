Accessing Data 
==============

Now that we have connected our Java application to a MySQL database, we need to set up our Java classes and interfaces.
In the previous chapters, we learned about performing CRUD operations on a database and its tables.
One of the reasons we use ORM is so that now we can write Java code in our application to manage our relational database.

.. index:: ! persistent class, ! entity class, ! @Entity, ! @Id, ! @GeneratedValue

Persistent Classes
------------------

Our JPA needs to know what Java class is going to be converted to a table in the MySQL database.
A Java class that models a persistent data store is called a **persistent class** or **entity class**.

``@Entity`` denotes an entity class. Entity classes look very similar to any other Java class, *except* entity classes have *two* constructors.
One is the one you need to create an instance of the class. 
The second one is ``protected`` and has no arguments and/or no return statement.
While you have to make sure you set up this second constructor, this constructor will only be used by the JPA.

Since an entity class determines the *structure* of a table in our relational database, you might want to add fields to the class to create ids and primary keys.
``@Id`` is an annotation that denotes that an integer id field is to be used as an id in the corresponding table in the database.
``@GeneratedValue`` is used in conjunction with the ``@Id`` annotation to create a primary key for the entity.

.. index:: ! repository, ! @Repository, ! CrudRepository

Repositories
------------

If entity classes determine the structure of a table in our relational database, we need to use a **repository** to get at the data *in* the table. 
Repositories are *not* models and are stored in a separate folder from models. Repositories are also interfaces, *not* classes.
We use the ``@Repository`` annotation to denote a repository.

When we create repository interfaces, we are not going to be extending a particular class. Instead, we will be extending ``CrudRepository``.
Extending the ``CrudRepository`` interface gives us access to methods to perform all of the CRUD operations that we made happen in SQL.

.. admonition:: Note

   ``CrudRepository`` has a number of different methods. You might want to bookmark the `documentation <https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html>`_ for later reference about the different methods.

Creating Persistent Models - Video
----------------------------------

.. raw:: html

   <div style="text-align:center;"><iframe width="560" height="315" src="https://www.youtube.com/embed/YAISqYMOIAw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

Creating Persistent Models - Text
---------------------------------

Now that we have connected MySQL and ``coding-events``, we are going to create a persistent class and a repository.

Let's create a persistent class for an event called ``Events``.

``Events`` has the following fields:

#. ``id``
#. ``name``
#. ``description``
#. ``contactemail``
#. ``type``

``Events`` also has all of the getters and setters for these fields and *both* constructors.

After making ``Events``, we can add a repository to ``data`` called ``EventRepository``.
``EventRepository`` extends ``CrudRepository``. We will add more methods and info to ``EventRepository`` soon.

Check Your Understanding
------------------------

.. admonition:: Question

   Entity classes are _________ and repositories are ____________.

   A. classes, interfaces
   B. interfaces, classes
   C. classes, classes
   D. interfaces, interfaces
