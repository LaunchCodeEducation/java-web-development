Exercise Solutions: SQL, Part 1
===============================

Create
------

Open up a new query tab for the SQL commands you code in this section.

#. Use the following SQL command to add a new entry to the ``seeds`` table.

   .. sourcecode:: SQL
      :linenos:

      INSERT INTO seeds (crop, encourages, use_by)
      VALUES ("Agastache", "bees & hummingbirds", 2020);

   Notice that you do NOT need to provide a value for ``seed_id``, since it is
   set up to auto-increment every time a new record is created.

3. To add values to only *some* of the columns of the table, simply omit those
   column names and values from the SQL command.

   .. sourcecode:: SQL
      :linenos:

      INSERT INTO seeds (crop, use_by)
      VALUES ("Sun Gold Tomato", 2022);

Read
----

Open up a new query tab for the SQL commands you code in this section.

#. Use ``SELECT ... FROM ...`` to list all of the data for all of the columns
   in the ``seeds`` table.

   .. sourcecode:: sql

      SELECT * FROM seeds;

3. List the ``crop`` and ``use_by`` data, and use ``ORDER BY`` to organize
   the information in *DECREASING* order by year.

   a. *Bonus*: For entries with matching ``use_by`` values, order first by
      year and then alphabetically by crop name.

   .. sourcecode:: sql

      SELECT crop, use_by
      FROM seeds
      ORDER BY use_by DESC, crop ASC;
   
Update
------

#. Update a single record based on its ``seed_id``.

   a. The first entry we added in the Create section has ``seed_id`` = 1. Use
      ``UPDATE ... SET ... WHERE`` to change the ``use_by`` date for this entry
      to 2024.
   b. Use a single ``UPDATE`` statement to change two columns for the entry
      with ``seed_id`` = 4.

   .. sourcecode:: sql

      UPDATE seeds
      SET use_by = 2024
      WHERE seed_id = 1;

#. With a single ``UPDATE`` command, set the ``expired`` value to ``true`` for
   all entries that have a ``use_by`` of this year or earlier.

   .. sourcecode:: sql

      UPDATE seeds
      SET expired = true
      WHERE use_by <= 2019;
   
Delete
------

#. Delete a single record from the table. Be sure to use its ``seed_id`` rather
   than any other column value in the ``WHERE`` clause.

   .. sourcecode:: sql

      DELETE FROM seeds WHERE seed_id = 4;