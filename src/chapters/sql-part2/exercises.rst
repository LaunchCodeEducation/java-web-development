Exercises: The SQL Sequel
=========================

In the previous chapter's exercises, we set up a database to store information about seeds. Let's expand that idea now that we know all about foreign keys!

Create a New Schema
-------------------

To get started, let's set up a :ref:`new schema <sql-part1-exercises>` in MySQL Workbench and call it ``garden``.
In the last chapter, we learned we can do this by clicking on *New Schema*, naming it ``garden``, accepting the defaults, and clicking *Apply*.

Import New Tables
-----------------

The starter data for these exercises is in the `Github repo <https://github.com/LaunchCodeEducation/java-web-development-starter-data>`_ under ``lesson-15-exercises``.
To import the data in our ``.csv`` files, we need to create three empty tables. Once you have created your tables, you need to use the :ref:`Table Import Wizard <table-import-data>`.

.. admonition:: Note

   The instructions state that you should be creating each table in separate query tabs. 
   If it works better for you and your workflow, feel free to create the three tables in one query tab!

The ``plant`` Table
^^^^^^^^^^^^^^^^^^^

Our first table is ``plant``. ``plant`` needs to have four columns:

#. ``plant_id``, which will be the primary key for our database.
#. ``plant_name``, which will contain the name of the plant.
#. ``zone`` is an integer for the hardiness zone where our plant will grow best.
#. ``season`` is a string that specifies the season when the plant blooms.

In a new query tab, use ``CREATE TABLE`` to make the ``plant`` table.
The data for the ``plant`` table is in the ``plants.csv`` file. You can download it directly from Github.

The ``seeds`` Table
^^^^^^^^^^^^^^^^^^^

Our second table is ``seeds``. ``seeds`` needs to have five columns:

#. ``seed_id``, which will auto increment.
#. ``expiration_date``, which will be of the ``DATE`` type.
#. ``quantity`` is an integer for the number of seeds we have available.
#. ``reorder`` of type ``BOOL`` and tells us if we need to reorder that type of seed.
#. ``plant_id`` is the foreign key that connects ``seeds`` to ``plant``.

In a new query tab, use ``CREATE TABLE`` to make the ``seeds`` table.
The data for the ``seeds`` table is in the ``seeds.csv`` file. You can download it directly from Github.

The ``garden_bed`` Table
^^^^^^^^^^^^^^^^^^^^^^^^

Our third table is ``garden_bed``. ``garden_bed`` needs to have four columns:

#. ``space_number``, which will increment as we plant new plants.
#. ``date_planted`` of type ``DATE`` for the day that we started the plant.
#. ``doing_well`` of type ``BOOL`` and tells us if the plant is healthy and growing.
#. ``plant_id`` is the foreign key that connects ``garden_bed`` to ``plant``.

In a new query tab, use ``CREATE TABLE`` to make the ``garden_bed`` table.
The data for the ``garden_bed`` table is in the ``garden.csv`` file. You can download it directly from Github.

Try Out Some Joins!
-------------------

Before we jump in with our subqueries and more complex queries, let's practice our joins from the previous chapter.
After you write each query, look at the result set and reflect on why that information might be helpful.
If you needed this database to manage your own garden, how would you use the result set?

Inner Join
^^^^^^^^^^

Use an inner join on ``seeds`` and ``garden_bed`` to see which plants we have seeds for and are in our garden bed.

Left Join
^^^^^^^^^

Write a query that joins ``seeds`` and ``garden_bed`` with a left join to see all of the seeds we have and any matching plants in the garden bed.

Right Join
^^^^^^^^^^

Write a query that joins ``seeds`` and ``garden_bed`` with a right join to see all the plants in the garden bed and any matching seeds we have.

Full Join
^^^^^^^^^

Write a query that joins ``seeds`` and ``garden_bed`` with a full join.

.. admonition:: Note

   In the previous chapter, we learned that MySQL does not support full joins.
   Review the section on :ref:`full joins <fullouterjoin>` to see how this could be done!

Sub-Queries and Complex Queries
-------------------------------

#. When we were writing our joins, you may have noticed that the information that was most helpful to you (the ``plant_name``) was missing from the result set! Write a query that gets the name of the plant by joining the ``plant`` table on the result set of the inner join query above. *Hint*: Open the query tab with the inner join query and copy it into a new query tab to start. Once you have your inner join setup in a new query tab, it will be easier to write your subquery.
#. Let's say our ``plant`` table is so large that we have no idea what the ``plant_id`` for a hosta is. All we know is that there is definitely a row for hostas in the ``plant`` table. Write a query that will insert a new row into our ``seeds`` table. This new row needs to show that we received 100 hosta seeds that will expire on 08/05/2020 (so no need to reorder!) and for the ``plant_id``, use a query *inside* the INSERT statement to get the appropriate ID for hostas. *Hint*: In order to get the ``plant_id`` of a hosta, you can use the following query in one line ``SELECT plant_id FROM plant WHERE (plant_name LIKE 'Hosta')`` inside the ``VALUES`` of the ``INSERT`` statement.

Bonus Missions
--------------

#. Revisit your query with a full join and try using ``UNION ALL`` as opposed to ``UNION``. How does the result set differ?
#. Now that we can get the ``plant_name`` of plants that we have seeds for and are in the garden bed, try using ``COUNT()`` to see how many plants are in both places.
