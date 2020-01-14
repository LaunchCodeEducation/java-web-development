Accessing Data 
==============

Now that we have set up our Java application to connect with a MySQL database, we need to set up the appropriate Java code.
In the previous chapters, we learned about performing CRUD operations on a database and the info inside a table in order to manage it.
One of the reasons we use ORM is so that we can write Java code in our application to manage our relational database.

.. index:: ! persistent class, ! entity class, ! @Entity, ! @Id, ! @GeneratedValue

Persistent Classes
------------------

Our JPA needs to know what Java class is going to be converted to a table in the MySQL database.
A Java class that is models a persistent data store is called a **persistent class** or **entity class**.

``@Entity`` denotes an entity class. Entity classes look very similar to any other Java class, *except* entity classes have *two* constructors.
One is the one you need to create an instance of the class. 
The second one is ``protected`` and has no arguments and/or no return statement.
While you have to make sure you set up this second constructor, this constructor will only be used by the JPA.

Since an entity class determines the *structure* of a table in our relational database, you might want to add fields to the class to create ids and primary keys.
``@Id`` is an annotation that denotes that an integer id field is to be used as an id in the corresponding table in the database.
``@GeneratedValue`` is used in conjunction with the ``@Id`` annotation to create a primary key for the entity.

.. index:: ! data access object, ! repository, ! @Repository

Data Access Objects
-------------------

If entity classes determine the structure of a table in our relational database, we need to use a **data access object** or **repository** to get at the data *in* the table. 
A repository is an interface stored in a separate folder from our models. Repositories are *not* models.
We use the ``@Repository`` annotation to denote a repository.

When we create repository interfaces, we are not going to be extending a particular class. Instead, we will be extending ``CrudRepository``.
Extending the ``CrudRepository`` interface gives us access to methods to perform all of the CRUD operations that we made happen in SQL.

Creating Persistent Models - Video
----------------------------------

.. raw:: html

   <div style="text-align:center;"><iframe width="560" height="315" src="https://www.youtube.com/embed/YAISqYMOIAw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

Creating Persistent Models - Text
---------------------------------


Additional Annotations
----------------------

``@Transactional``

``@OneToMany``

``@JoinColumn``

``@ManyToOne``

Check Your Understanding
------------------------