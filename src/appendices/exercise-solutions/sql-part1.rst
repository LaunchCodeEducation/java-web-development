.. _sql-part1-exercise-solutions:

Exercise Solutions: SQL, Part 1
===============================

.. _sql-part1-exercise-solutions-create:

Create
------

Here is an example of how the query tab might look after adding different records:

.. sourcecode:: sql
   :linenos:

   INSERT INTO seeds (crop, encourages, use_by)
   VALUES ("Agastache", "bees & hummingbirds", 2020);

   INSERT INTO seeds (crop, encourages, use_by)
   VALUES ("Broccoli", "health", 2019);

   INSERT INTO seeds (crop, use_by)
   VALUES ("Sun Gold Tomato", 2022);

   INSERT INTO seeds (crop, encourages, use_by)
   VALUES ("Zinnia", "bees", 2020);

   INSERT INTO seeds (crop)
   VALUES ("Rutabaga");

   INSERT INTO seeds (crop, use_by)
   VALUES ("Sun Gold Tomato", 2024);

   INSERT INTO seeds (crop, encourages, use_by)
   VALUES ("Green Beans", "Cucumber", 2020);

:ref:`Back to the exercises <sql-part1-exercises>`

.. _sql-part1-exercise-solutions-read1:

Read
----

Open up a new query tab for the SQL commands you code in this section.

#. Use ``SELECT ... FROM ...`` to list all of the data for all of the columns
   in the ``seeds`` table.

   .. sourcecode:: sql

      SELECT * FROM seeds;

   :ref:`Back to the exercises <sql-part1-exercises>`

.. _sql-part1-exercise-solutions-read3:

3. List the ``crop`` and ``use_by`` data, and use ``ORDER BY`` to organize
   the information in *DECREASING* order by year.

   a. *Bonus*: For entries with matching ``use_by`` values, order first by
      year and then alphabetically by crop name.

   .. sourcecode:: sql

      SELECT crop, use_by
      FROM seeds
      ORDER BY use_by DESC, crop ASC;

   :ref:`Back to the exercises <sql-part1-exercises>`

.. _sql-part1-exercise-solutions-update1:

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

   :ref:`Back to the exercises <sql-part1-exercises>`

.. _sql-part1-exercise-solutions-update3:

3. With a single ``UPDATE`` command, set the ``expired`` value to ``true`` for
   all entries that have a ``use_by`` of this year or earlier.

   .. sourcecode:: sql

      UPDATE seeds
      SET expired = true
      WHERE use_by <= 2019;
   
   :ref:`Back to the exercises <sql-part1-exercises>`

.. _sql-part1-exercise-solutions-delete:

Delete
------

#. Delete a single record from the table. Be sure to use its ``seed_id`` rather
   than any other column value in the ``WHERE`` clause.

   .. sourcecode:: sql

      DELETE FROM seeds WHERE seed_id = 4;

   :ref:`Back to the exercises <sql-part1-exercises>`