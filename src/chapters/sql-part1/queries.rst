SQL Queries
===========

.. index:: ! query, ! CRUD, ! result set

When we want to perform an operation on a database, we write a SQL **query**.
Queries can vary widely in complexity and purpose depending on the operation we need to perform.
Each query produces a **result set** containing the requested data.
Ultimately, we can boil down each query's purpose into one of the following four categories:

#. Create
#. Read
#. Update
#. Delete

**CRUD** or *Create*, *Read*, *Update*, *Delete* represents the four major operations we perform when we work with data.
Let's see how we can do this with SQL!

.. admonition:: Note

   Throughout the rest of the chapter, we will be using an example of an events database.
   Our event planner, Mary, has a database storing the guest info of every event she has ever planned, as well as event info about each event.
   She named each table of guest info after the event itself.

Create
------

When we talk about creating something in SQL, we could want to perform several operations.
We may want to create a table, add a row, or add a column.

Creating a Table
^^^^^^^^^^^^^^^^

Creating a Table from Scratch
"""""""""""""""""""""""""""""

Let's say that we are working on our events database.
Mary has been working hard planning the Li wedding.
She wants us to create a table with the pertinent guest info of every guest invited.
Each row will represent one guest.
The columns include the unique number id for each guest, the guest's first name, their last name, their dietary preferences, and whether or not they will be in attendance.

To add a table to our database for the Li wedding, we need to use the ``CREATE TABLE`` command.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE LiWedding (
      GuestID int,
      LastName varchar(255),
      FirstName varchar(255),
      Attending BOOL,
      Diet varchar(255)  
   );

This query creates a new table in our database called ``LiWedding``. This table contains five columns: ``GuestID`` of type ``int``, ``LastName`` of type ``varchar(255)``, ``FirstName`` of type ``varchar(255)``, ``Attending`` of type ``BOOL``, ``Diet`` of type ``varchar(255)``.
When we use ``CREATE TABLE`` to create a table from scratch, we will end up with an empty table. We will learn how to add to a table a little further down the page.

Creating a Table from Another Table
"""""""""""""""""""""""""""""""""""

We can also create a table from another table.
When doing so, the new table will also include any existing data from the original table.

Mary is also planning a vow renewal for Mr. and Mrs. Johnson.
Since the Johnsons haven't made any new friends in the past 5 years, they want the guest list to be the exact same.
A good place to start would be to create a table called ``JohnsonVowRenewal`` from the table called ``JohnsonWedding``.
Due to some wedding drama, Mr. and Mrs. Johnson will also be avoiding inviting anyone who didn't show up for the first wedding.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE JohnsonVowRenewal
   AS GuestID, LastName, FirstName, Attending, Diet
   FROM JohnsonWedding
   WHERE (Attending == 1);

This query creates the ``JohnsonVowRenewal`` table with the same columns as ``JohnsonWedding``.
We use ``AS`` to specify the columns that will be carried over from the ``JohnsonWedding`` table to the ``JohnsonVowRenewal``.
The ``WHERE`` condition in the query specifies that we only want the rows from ``JohnsonWedding`` in ``JohnsonVowRenewal`` *where* the guest was in attendance (or ``Attending == 1``).
If we did *not* add a ``WHERE`` condition, then we would have copied over all of the data from ``JohnsonWedding``.

Adding a Row
^^^^^^^^^^^^

Whether we have created a table from scratch or are working with an existing table, we may need to add a row of data.
To do so, we need to use an ``INSERT INTO`` statement.

In the case of the Johnsons, we may need to add a row for their niece, who is now old enough to attend the vow renewal.
Their niece is Eliza Johnson and she is a vegan. Her mother has also confirmed that she will be in attendance.

.. sourcecode:: mysql

   INSERT INTO JohnsonVowRenewal
   VALUES (185, "Johnson", "Eliza", 1, "Vegan");

This query adds a row for Eliza to the ``JohnsonVowRenewal`` table in our database.

If we wanted to add a row, but only add values to specific columns in the table, we can do so! We simply need to add the names of the columns that we will be adding data to.

In the case of inviting people the Johnson's vow renewal, we may want to invite Eliza's sister, Felicity, as well. However, we do not have confirmed Felicity's dietary preferences or whether or not she is coming.

.. sourcecode:: mysql

   INSERT INTO JohnsonVowRenewal (GuestID, LastName, FirstName)
   VALUES (186, "Johnson", "Felicity");

By adding the column names in parantheses after the table name, we have specified that we are adding a new row of data to the table, but we only have values for the columns: ``GuestID``, ``LastName``, and ``FirstName``.

.. admonition:: Note

   When we use this method, any column that doesn't have a specified value for the new row will have a ``null`` value. 

Adding a column
^^^^^^^^^^^^^^^

Sometimes, we may also need to add a column to our table. Some of the caterers Mary works with have asked that she confirm how many people are of drinking age.
We may now want to add a column to our ``LiWedding`` table that contains either ``1`` or ``0`` depending on whether the guest is legally old enough to drink.

To add a column, we need to start with an ``ALTER TABLE`` statement. ``ALTER TABLE`` can be used to perform different operations, so in our case, we will also need to specify that we want to ``ADD`` a column.

.. sourcecode:: mysql

   ALTER TABLE LiWedding
   ADD CanDrink boolean;

This adds the ``CanDrink`` column to the ``LiWedding`` table, but it does *not* fill that column with values. We will need to update each guest's entry in the table once we confirm how old they are.

.. admonition:: Note

   For more on the ``ALTER TABLE`` statement and how many different ways it can be used, check out `w3schools <https://www.w3schools.com/sql/sql_alter.asp>`_.

Read
----

When reading data, we don't want to modify anything, we just want to know what is there. 
In order to get information from a table, we need to use a ``SELECT`` statement. 

``SELECT`` statements have a few different components to them. We need to know what we are selecting, which table the information is in, and if necessary, we can also use ``WHERE`` to apply a conditional.
In general, ``SELECT`` statements look like the following:

.. sourcecode:: mysql

   SELECT ColumnName1, ColumnName2, ...
   FROM TableName
   WHERE some conditional is true.

If Mary wants to get the information of all of the guests who are vegetarian at the Li wedding, we need to use a ``SELECT`` statement to pull the first and last names of guests who will be in attendance and are vegetarian.
So, we will ``SELECT`` the ``LastName`` and ``FirstName`` columns ``FROM`` the ``LiWedding`` table ``WHERE`` the value of ``Attending`` is ``TRUE`` and the value of ``Diet`` is ``"vegetarian"``.

.. sourcecode:: mysql
   :linenos:

   SELECT LastName, FirstName
   FROM LiWedding
   WHERE (Attending == 0) AND (Diet == "vegetarian");

If Mary just wants all of the guests for the Li wedding, we need to modify our ``SELECT`` statement.
We won't apply a ``WHERE`` condition to our query and we will use a ``*`` to denote that we want all columns.

.. sourcecode:: mysql

   SELECT *
   FROM LiWedding;

Update
------

Now that we can add data and see what our data actually is, let's start changing it!

.. admonition:: Warning

   Updating a table is something that we want to be cautious when doing.
   We cannot simply click *Edit* > *Undo* if we make a mistake!

Earlier, we made a mistake! Eliza is a vegetarian, but not a vegan. We want to update the record in the ``JohnsonVowRenewal`` table.

.. sourcecode:: mysql 

   UPDATE JohnsonVowRenewal
   SET Diet="vegetarian"
   WHERE GuestID==185;

Now if we use a ``SELECT`` statement, we can confirm that we have properly updated the record.

.. sourcecode:: mysql

   SELECT *
   FROM JohnsonVowRenewal
   WHERE GuestID==185;

Delete
------

Our final operation we may want to perform on a table is to delete something.

.. admonition:: Warning

   Deleting a record permanently removes it from the table!
   Proceed with caution with removing records!

Mr. Johnson's great-uncle, Frank, died and won't be in attendance for the vow renewal. Since he was in attendance at their wedding, when we created ``JohnsonVowRenewal`` from ``JohnsonWedding``, Frank's record needs to be removed.

.. sourcecode:: mysql

   DELETE FROM JohnsonVowRenewal WHERE GuestID==107;

We can then use a ``SELECT`` statement to confirm that Uncle Frank's record has been removed.

.. sourcecode:: mysql

   SELECT *
   FROM JohnsonVowRenewal
   WHERE GuestID==107;

Check Your Understanding
------------------------

.. admonition:: Question

   What does the following query do?

   .. sourcecode:: mysql

      SELECT EventID
      FROM EventsMaster
      WHERE (Month==07);

   a. Returns the event id from a table called ``EventsMaster`` for all events in 7 months of the year.
   b. Returns the event id for all events in a table called ``EventsMaster`` for the month of July.
   c. Returns the event id for all events in a table called ``EventsMaster`` for the month of June.

.. ans: b

.. admonition:: Question

   Mary has hired another event planner, Leah.
   We now need to create a table for the events that Leah is going to be planning.
   We also need to add a row for her first clients, Tate and Carlos.
   Does the following query accomplish this task?

   .. sourcecode:: mysql
      :linenos:

      CREATE TABLE LeahEvents (
         EventID int,
         EventName varchar(255),
         Month int,
         Day int,
         Year int
      );

      INSERT INTO LeahEvents
      VALUES (256, "SmithWedding", 08, 08, 2021);

.. ans: Yes, it does!
