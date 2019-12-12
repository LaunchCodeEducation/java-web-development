Exercises: SQL, Part 1
======================

In order to practice SQL commands, you must first set up a new database (model)
on your computer. In the MySQLWorkbench program, each new model is called a
*schema*.

#. Open MySQLWorkbench and open a connection. You may be prompted once or twice
   for passwords, depending on how you set up your root.

   .. figure:: ./figures/mswHomeScreen.png
      :alt: MySQLWorkbench home screen.
      :scale: 60%

#. Click on the *Create New Schema* button and give the database a distinctive
   name.

   .. figure:: ./figures/createNewSchemaButton.png
      :alt: Create new schema button.

#. Click *Apply*, and accept all of the default options when prompted. You
   should see the new database when you click the *Schemas* tab.

   .. figure:: ./figures/practiceSchema.png
      :alt: New practice database in the file tree.
      :scale: 80%

#. Your new database is *almost* ready to use. The last step is to set the
   model as the default option for SQL commands. Do this by double-clicking its
   name in the file tree.

Good. You are set up for this lesson's practice. Complete the following
exercises in the *Query* tab of MySQLWorkbench.

.. admonition:: Tip

   If you have questions about how to use MySQLWorkbench, do not hesitate to
   reference `the documentation <https://dev.mysql.com/doc/workbench/en/wb-home.html>`__.

Create
------

Add 3 - 4 new entries to the table with INSERT INTO.

#. Using values for all fields (syntax 1),
#. Using values for only specific fields (syntax 2).
#. Paste code sample to include additional data.

Read
----

Open up a new query tab...

Perform several list actions.

#. List all data in table, including repeats.
#. List all data in table, excluding repeats.
#. List specific columns from the table.
#. List all columns by ID request.
#. Provide conditions using WHERE and logical operators.
#. Practice using ORDER BY.

Update
------

Open up a new query tab...

#. Update a single record based on ID.
#. Update a set of records based on a more general condition.
#. Add a new column to the table.
#. (Bonus) Experiment with changing the data type of a column (link).

Delete
------

Open up a new query tab...

WARNINGS!!!!

#. Delete a single record from the table.
#. Delete a set of records from the table.
#. DROP table vs. DELETE FROM table.

Joins
-----

Open up a new query tab...

Create a new table with foreign key linked to 1st table.

Populate new table with data (paste in SQL script).

Inner Join
^^^^^^^^^^

#. Do this (provide syntax).
#. Compare result with original tables.

Left Join
^^^^^^^^^

#. Do this (provide syntax).
#. Compare result with original tables.

Right Join
^^^^^^^^^^

#. Do this (provide syntax).
#. Compare result with original tables.

Full Join
^^^^^^^^^

#. Do this (provide syntax).
#. Compare result with original tables.
