What is SQL?
============

.. index:: ! relational database, ! Structured Query Language, ! SQL, ! Relational Database Management System, ! RDMS

Previously, we learned about how we use the model in our MVC applications to handle data.
Now, we want to attach a *persistent* data source that will sit on a server waiting for the model to perform actions.
This is where a relational database comes in.

**Relational databases** store data in tables, which are connected to each other in a variety of different ways.
Tables contain columns and rows of information, with each column specifying the data type of the information within, and each row having a unique key.
Relational databases provide flexibility for both expansion of the database and modification of the relationships between the tables as things change.

In order to access our information, we need to use a tool that can talk to a relational database. 
**Structured Query Language** or **SQL** is the main tool used by programmers to work with these data structures.
SQL is a **Relational Database Management System** or **RDMS**. 
We can use SQL to perform many essential operations on a database, such as adding and removing data.

MySQL
-----

There are many different types of SQL. For this class, we will be using `MySQL <https://dev.mysql.com/>`_.
MySQL is open-source and user-friendly.

To get started with the chapter, you need to :ref:`install MySQL <sql-installation>` and the appropriate tooling.

MySQL has many of the same data types as Java. However, some of the types, like ``String``, have a different name in MySQL.

Numbers
^^^^^^^

For integers, we will be using the ``INT`` data type. As you grow in your career, you may see others such as ``BIGINT`` or ``MEDIUMINT`` in MySQL databases.
The `MySQL documentation <https://dev.mysql.com/doc/refman/8.0/en/integer-types.html>`_ offers a full breakdown of these different integer types.

MySQL also has a ``DOUBLE`` data type that is similar to what we have already worked with in Java. 

Strings
^^^^^^^

There is no ``STRING`` type in MySQL.
Instead, we use the ``VARCHAR`` type.
``VARCHAR`` produces a string of variable length, but we have to tell MySQL how long the string will be *at a maximum*.
Therefore, when we use ``VARCHAR`` in a declaration, we add the maximum number of characters like so: ``VARCHAR(250)``. That declaration specifies that the string will be, at a maximum, 250 characters.

Boolean
^^^^^^^

MySQL does not officially support boolean values such as ``TRUE`` or ``FALSE``. To make things a little easier for us and other SQL developers, they do have data types called ``BOOL`` and ``BOOLEAN``.
``BOOL`` and ``BOOLEAN`` are synonyms for the ``TINYINT`` type, with 0 counting as ``FALSE`` and non-zero values (such as 1) counting as ``TRUE``.

Check Your Understanding
------------------------

.. admonition:: Question

   Which of the following are supported data types in MySQL? Select ALL that are correct.

   A. ``TINYINT``
   B. ``INTEGER``
   C. ``DOUBLE``
   D. ``VARCHAR``
   E. ``BOOLEAN``
   F. ``STRING``

