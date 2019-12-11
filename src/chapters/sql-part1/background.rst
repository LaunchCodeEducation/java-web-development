What is SQL?
============

.. index:: ! relational database, ! Structured Query Language, ! SQL

Previously, we learned about how we use the model in our MVC applications to handle data.
Now, we want to attach a *persistent* data source that will sit on a server waiting for the model to perform actions.
This is where a relational database comes in.

**Relational databases** store data in tables, which are connected to each other in a variety of different ways to form a database.
Tables contain columns and rows of information with each row having a unique key and each column specifying the data type of the information within.
Relational databases provide flexibility for both expansion of the database and modification of the relations as things change.

In order to access our information, we need to use a tool that can talk to a relational database. 
**Structured Query Language** or **SQL** is the main tool used by programmers to work with these data structures.
SQL is a **Relational Database Management System** or **RDMS**. 
We can use SQL to perform CRUD operations on a database, combine two tables, and many other important operations.

MySQL
-----

There are many different types of SQL. For this class, we will be using `MySQL <https://dev.mysql.com/>`_.
MySQL is open-source and user-friendly.

.. TODO: Add link to SQL installation appendix

To get started with the chapter, you need to install MySQL and the appropriate tooling.