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
The first constructor creates an instance of the class. 
The second one is ``protected`` and has no arguments and/or no return statement.
While you must set up this second constructor, it will only be used by the JPA to create a new instance.

Since an entity class determines the *structure* of a table in our relational database, you can add fields to the class to create ids and primary keys.
``@Id`` is an annotation that denotes that an integer id field is to be used as an id in the corresponding table in the database.
``@GeneratedValue`` is used in conjunction with the ``@Id`` annotation to create a primary key for the entity.

.. admonition:: Example

   In the case of the previous example, we want to make our ``ContactInfo`` class an entity class.

   .. sourcecode:: java
      :linenos:

      @Entity
      public class ContactInfo {
         @Id
         @GeneratedValue
         private int id;

         private String name;

         private String email;

         public ContactInfo(String n, String e) {
            this.name = n;
            this.email = e;
         }

         public ContactInfo() {} 
      }

   This class declaration makes use of ``@Id`` and ``@GeneratedValue`` for the ``id`` field. Every time we instantiate a new object of the ``ContactInfo`` class, the object will have an id that translates to the primary key of the ``contactinfo`` table.
   We also have two constructors: the first is what we will use to instantiate an object for Frank, and the second is what the JPA uses to instantiate an object.

.. index:: ! repository, ! @Repository, ! CrudRepository

Repositories
------------

While entity classes determine the structure of a table in our relational database, a **repository** gets at the data *in* the table. 
Repositories are *not* models and are stored in a separate folder from models. Repositories are also interfaces, *not* classes.
We use the ``@Repository`` annotation to denote a repository.

When we create repository interfaces, we are not going to be extending a particular class. Instead, we will be extending ``CrudRepository``.
Extending the ``CrudRepository`` interface gives us access to methods to perform all of the CRUD operations that we made happen in SQL.

.. admonition:: Note

   ``CrudRepository`` has a number of different methods. You might want to bookmark the `documentation <https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html>`_ for later reference about the different methods.

.. admonition:: Example

   To get at the data in the ``contactinfo`` table, we need to create a ``ContactInfoRepository`` interface.

   .. sourcecode:: java
      :linenos:

      @Repository
      public interface ContactInfoRepository extends CrudRepository<ContactInfo, Integer> {
      }

   This code creates a repository called ``ContactInfoRepository`` so we can fetch data from the ``contactinfo`` table.
   
On the next page, we will cover how to use a controller and ``CrudRepository`` methods to get info in and out of the tables of our relational database.

Creating Persistent Models - Video
----------------------------------

The following video explains how we can add an entity class and a repository to our ``coding-events`` application. 
The accompanying text is a quick rundown of what happens in the video. To get started, create a branch off of your `db-config <https://github.com/LaunchCodeEducation/coding-events/tree/db-config>`_ branch.

.. youtube::
   :video_id: YAISqYMOIAw
   :gh_path: LaunchCodeEducation/coding-events/persistent-models

Creating Persistent Models - Text
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In summary, now that we have connected MySQL and ``coding-events``, let's create a persistent class and a repository.

Create a persistent class for an event called ``Events``.

Create the following fields for ``Events``:

#. ``id``
#. ``name``
#. ``description``
#. ``contactemail``
#. ``type``

For ``Events``, create all of the getters and setters for these fields and *both* constructors.

After making ``Events``, we can add a repository to ``data`` called ``EventRepository``.
``EventRepository`` extends ``CrudRepository``. We will add more methods and info to make use of ``EventRepository`` soon.

Check Your Understanding
------------------------

.. admonition:: Question

   Entity classes are _________ and repositories are ____________.

   A. classes, interfaces
   B. interfaces, classes
   C. classes, classes
   D. interfaces, interfaces

.. ans: A
