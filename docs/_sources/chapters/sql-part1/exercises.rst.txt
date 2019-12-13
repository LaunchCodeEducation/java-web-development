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

Table Setup
-----------

For these exercises, we will use a ``seeds`` table to store information for our
garden hopes. The table will have 4 columns:

#. ``seed_id``: This is a unique number assigned to each row in the ``seeds``
   table.
#. ``crop``: Identifies what the seeds grow (e.g. yellow bell peppers).
#. ``encourages``: Identifies the benefits of planting the crop (e.g. nitrogen
   fixation, attracts bees, etc.)
#. ``use_by``: The year the seeds expire.

The the ``crop`` and ``encourages`` columns will hold string data types,
``seed_id`` and ``use_by`` will be integers.

Paste the following script into the query tab, then run it.

.. sourcecode:: SQL
   :linenos:

   CREATE TABLE seeds (
      seed_id INTEGER PRIMARY KEY AUTO_INCREMENT,
      crop VARCHAR(40),
      encourages VARCHAR(80),
      use_by INTEGER
   );

Note that the SQL syntax for string data types is ``VARCHAR``, and it includes
a parameter that specifies the maximum length of the string.

Properly done, you should now see the ``seeds`` table within your database.

.. figure:: ./figures/seedsTableFileTree.png
   :alt: File tree for the seeds table.

Create
------

Open up a new query tab for the SQL commands you code in this section.

.. admonition:: Tip

   MySQLWorkbench allows you to run one SQL command, a set of commands, or all
   of the commands listed in the editor pane. Hover over each lightning bolt
   icon in the panel to see these options.

   .. figure:: ./figures/workbenchBoltIcons.png
      :alt: Lightning bold icons in MySQLWorkbench.

#. Use the following SQL command to add a new entry to the ``seeds`` table.

   .. sourcecode:: SQL
      :linenos:

      INSERT INTO seeds (crop, encourages, use_by)
      VALUES ("Agastache", "bees & hummingbirds", 2020);

   Notice that you do NOT need to provide a value for ``seed_id``, since it is
   set up to auto-increment every time a new record is created.

   .. admonition:: Tip

      At any time, you can confirm that a table contains data by clicking on
      the table icon next to its name.

      .. figure:: ./figures/seedsTableCheck.png
         :alt: View table contents button.

#. Add another new entry to the ``seeds`` table, choosing your own values for
   the columns.
#. To add values to only *some* of the columns of the table, simply omit those
   column names and values from the SQL command.

   .. sourcecode:: SQL
      :linenos:

      INSERT INTO seeds (crop, use_by)
      VALUES ("Sun Gold Tomato", 2022);

#. Add 3 - 5 more records to the ``seeds`` table.

Note that ``null`` gets stored in a column whenever a value for that field is
not supplied.

Read
----

Open up a new query tab for the SQL commands you code in this section.

#. Use ``SELECT ... FROM ...`` to list all of the data for all of the columns
   in the ``seeds`` table. (*Hint*: Use the ``*`` wildcard instead of typing
   out all of the column names).
#. List ONLY the ``crop`` data from the table.
#. List the ``crop`` and ``use_by`` data, and use ``ORDER BY`` to organize
   the information in *DECREASING* order by year.

   a. *Bonus*: For entries with matching ``use_by`` values, order first by
      year and then alphabetically by crop name.

#. List the complete records for the seeds, but only if the ``encourages``
   column is not ``null``. You will need to include a ``WHERE`` in your SQL
   command.
#. List a single entry based on its ``seed_id`` value.

Update
------

Open up a new query tab for the SQL commands you code in this section.

.. admonition:: Warning

   The general syntax for a SQL update is:

   .. sourcecode:: bash

      UPDATE table_name
      SET column1 = newValue1, column2 = newValue2, ...
      WHERE condition;

   If you leave out the ``WHERE`` clause, then *ALL* records in the table will
   be updated!


#. Update a single record based on its ``seed_id``.

   a. The first entry we added in the Create section has ``seed_id`` = 1. Use
      ``UPDATE ... SET ... WHERE`` to change the ``use_by`` date for this entry
      to 2024.
   b. Use a single ``UPDATE`` statement to change two columns for the entry
      with ``seed_id`` = 4.

#. Use ``ALTER TABLE`` to add a new column, called ``expired``, to the table.
   Set the data type to ``boolean``.
#. With a single ``UPDATE`` command, set the ``expired`` value to ``true`` for
   all entries that have a ``use_by`` of this year or earlier.

Be sure to list the ``seeds`` table to confirm your changes.

Delete
------

Open up a new query tab for the SQL commands you code in this section.

.. admonition:: Warning

   If you leave out the ``WHERE`` clause in the ``DELETE FROM`` command, then
   *ALL* records in the table will be lost!

   There is no undo option after running ``DELETE``.

#. Delete a single record from the table. Be sure to use its ``seed_id`` rather
   than any other column value in the ``WHERE`` clause.
#. Use a single ``DELETE`` command to remove any seeds from the table that have
   expired.

Joins
-----

In order to complete the ``JOIN`` practice, you will need two new tables in
your database. Paste and run the following SQL script in a new query tab. It
will create and populate both tables.

.. sourcecode:: sql
   :linenos:

   CREATE TABLE seed_storage (
      seed_storage INTEGER PRIMARY KEY AUTO_INCREMENT,
      number_of_seeds INTEGER,
      drawer_number INTEGER,
      reorder BOOLEAN
   );

   CREATE TABLE veggie (
      veggie_id INTEGER PRIMARY KEY AUTO_INCREMENT,
      veggie_name VARCHAR(40),
      companion_plant VARCHAR(80),
      seed_storage INTEGER,
      FOREIGN KEY (seed_storage) REFERENCES seed_storage(seed_storage)
   );

   INSERT INTO seed_storage (number_of_seeds, drawer_number, reorder)
   VALUES (150, 22, number_of_seeds <= 25);

   INSERT INTO seed_storage (number_of_seeds, drawer_number,reorder)
   VALUES (500, 3, number_of_seeds <= 25);

   INSERT INTO seed_storage (number_of_seeds, drawer_number, reorder)
   VALUES (25, 18, number_of_seeds <= 25);

   INSERT INTO seed_storage (number_of_seeds, drawer_number, reorder)
   VALUES (5, 7, number_of_seeds <= 25);

   INSERT INTO veggie (veggie_name, companion_plant)
   VALUES ("Broccoli", "Celery");

   INSERT INTO veggie (veggie_name, companion_plant, seed_storage)
   VALUES ("Carrot", "Radishes & Tomatoes", 1);

   INSERT INTO veggie (veggie_name, companion_plant)
   VALUES ("Green Beans", "Spinach, Corn & Peas");

   INSERT INTO veggie (veggie_name, companion_plant, seed_storage)
   VALUES ("Rutabaga", "Dill & Sage", 3);


Note that the ``veggie`` table has a *foreign key* linked to ``seed_storage``.

Inner Join
^^^^^^^^^^

#. Run this SQL command in a new query tab.

   .. sourcecode:: sql
      :linenos:

      SELECT *
      FROM veggie
      INNER JOIN seed_storage ON seed_storage.seed_storage = veggie.seed_storage;

#. Note that the output shows only two results, even though the ``veggie`` and
   ``seed_storage`` tables each contain four records.
#. Summarize what ``INNER JOIN`` does.

.. admonition:: Note

   You can list specific columns by replacing ``*`` with a set of column names
   (e.g. ``SELECT veggie_name, drawer_number, number_of_seeds``).

Left Join
^^^^^^^^^

#. Run this SQL command in the same JOIN query tab.

   .. sourcecode:: sql
      :linenos:

      SELECT *
      FROM veggie
      LEFT JOIN seed_storage ON veggie.seed_storage = seed_storage.seed_storage;

#. Compare the output to the contents of the original ``veggie`` and
   ``seed_storage`` tables, then summarize what ``LEFT JOIN`` does.

Right Join
^^^^^^^^^^

#. Run this SQL command in the same JOIN query tab.

   .. sourcecode:: sql
      :linenos:

      SELECT *
      FROM veggie
      RIGHT JOIN seed_storage ON veggie.seed_storage = seed_storage.seed_storage;

#. Compare the output to the contents of the original ``veggie`` and
   ``seed_storage`` tables, then summarize what ``RIGHT JOIN`` does.

Bonus Exercises
---------------

Whew! You made it through all the exercises. Nice work!

Take a quick break and, if you wish, try these additional tasks that go above
and beyond the basic SQL commands.

#. Change any ``crop`` value of "Tomato" to "Tomahto", but make the update
   case-insensitive (e.g. tomato, TOMATO, and Tomato would all be changed to
   Tomahto).
#. Use logical operators (``AND``, ``OR``, ``NOT``) in ``WHERE`` statements.
#. Do you have several entries with the same ``crop`` value? If so, you can
   display a list that avoids repeats by using the `SELECT DISTINCT <https://www.w3schools.com/sql/sql_distinct.asp>`__
   keywords.
#. Experiment with `changing the data type <https://www.w3schools.com/sql/sql_alter.asp>`__
   of a column.
#. Explore the difference between ``DROP DATABASE table_name`` vs.
   ``DELETE FROM table_name``.
