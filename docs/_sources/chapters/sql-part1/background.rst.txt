What is SQL?
============

.. index:: ! relational database, ! Structured Query Language, ! SQL

Previously, we learned about how we use the model in our MVC applications to handle data.
Models in MVC applications can only handle data, but as the amount of data increases, the practicality of using a model to store it decreases.
This is where a relational database comes in.

**Relational databases** store data in tables.
Tables contain columns and rows of information with each row having a unique key.
Tables can then be connected to other tables in a variety of different ways to form a database.
Relational databases provide flexibility for both expansion of the database and modification of the relations as things change.

A table can in many ways look like a HashMap in Java.
HashMaps store a value for each key in the structure. 
A table stores values for each key in the strucutre.

In order to access our information, we need to use a tool that can talk to a relational database. 
**Structured Query Language** or **SQL** is the main tool used by programmers to work with these data structures.
Programmers designed SQL so they could ask questions of a database. We can use SQL to determine how many people are coming to an event, how many people are vegans, and how many people who we invited are unable to make it.