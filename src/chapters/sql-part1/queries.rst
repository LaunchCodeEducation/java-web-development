SQL Queries
===========

We want to be able to perform CRUD operations (Create, Read, Update, Delete) on a database and now we know that SQL can do that.
Let's dive into writing SQL queries to get the information we need.

Create
------

When we talk about creating something in SQL, we could want to perform several operations.

Creating a Table
^^^^^^^^^^^^^^^^

Let's say that we are working on our events database. We have a table with our guests for one event. But, we are working with a company that hosts dozens of events a month!
Now, Mary has asked us to add a table containing all of the guest information for the Li wedding.

To add a table to our database, we need to use the ``CREATE TABLE`` command.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE LiWedding (
      GuestID int,
      LastName varchar(255),
      FirstName varchar(255),
      Attending boolean,
      Diet varchar(255)  
   );

This creates an empty table with all of the spaces we need for guest info.

We can also create a table from another table. When doing so, the new table will also include any existing data.

Mary is also managing the second wedding of Mr. and Mrs. Johnson (it's a long story).
Since the Johnsons haven't made any new friends in the past 5 years, they want the guest list to be the exact same.
A good place to start would be to create a table called ``JohnsonWedding2`` from the table called ``JohnsonWedding``.
Mr. and Mrs. Johnson will also be avoiding inviting anyone who didn't show up for the first wedding.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE JohnsonWedding2
   AS GuestID, LastName, FirstName, Attending, Diet
   FROM JohnsonWedding
   WHERE (Attending == TRUE);

Adding a Row
^^^^^^^^^^^^

When we create a table from scratch, we have no data in it. We need to use an ``INSERT INTO`` statement to add a row of data. 

In the case of the Johnsons, we may need to add a row for their niece, who is now old enough to attend the wedding.
Their niece is Eliza Johnson and she is a vegan. Her mother has also confirmed that she will be in attendance.

.. sourcecode:: mysql

   INSERT INTO JohnsonWedding2
   VALUES (185, `Johnson`, `Eliza`, TRUE, `Vegan`);

Adding a column
^^^^^^^^^^^^^^^

Sometimes, we may also need to add a column to our table. Some of the caterers Mary works with have asked that she confirm how many people are of drinking age.
We may now want to add a column to our ``LiWedding`` table that contains either ``TRUE`` or ``FALSE`` depending on whether the guest is legally old enough to drink.

To add a column, we need to start with an ``ALTER TABLE`` statement. ``ALTER TABLE`` can be used to perform different operations, so in our case, we will also need to specify that we want to ``ADD`` a column.

.. sourcecode:: mysql

   ALTER TABLE LiWedding
   ADD CanDrink boolean;

Read
----

In order to get information from a table, we need to use a ``SELECT`` statement. 

If Mary wants to get the information of all of the guests who are vegetarian at the Li wedding, we need to use a ``SELECT`` statement to pull the first and last names of guests who will be in attendance and are vegetarian.

.. sourcecode:: mysql

   SELECT `LastName`, `FirstName`
   FROM LiWedding
   WHERE (Attending == TRUE) AND (Diet == "vegetarian");

If Mary just wants all of the guests for the Li wedding, we need to modify our ``SELECT`` statement.

.. sourcecode:: mysql

   SELECT *
   FROM LiWedding;

Update
------

Updating a table is something that we want to be cautious when doing.
We cannot go back from updating a table.

Earlier, we made a mistake! Eliza is a vegetarian, but not a vegan. We want to update the record in the ``JohnsonWedding2`` table.

.. sourcecode:: mysql 

   UPDATE JohnsonWedding2
   SET Diet=`Vegetarian`
   WHERE GuestID==185;

Now if we use a ``SELECT`` statement, we can confirm that we have properly updated the record.

.. sourcecode:: mysql

   SELECT *
   FROM JohnsonWedding2
   WHERE GuestID==185;

Delete
------

Our final operation we may want to perform on a table is to delete something.

Mr. Johnson's great-uncle, Frank, died and won't be in attendance. Since he was in attendance at their first wedding, when we created ``JohnsonWedding2`` from ``JohnsonWedding``, Frank's record needs to be removed.

.. sourcecode:: mysql

   DELETE FROM JohnsonWedding2 WHERE GuestID==107;


