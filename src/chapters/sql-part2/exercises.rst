Exercises: SQL, Part 2
=======================

In the previous chapter, we set up a database to store information about seeds. Let's expand that idea now that we know all about foreign keys!

Create a New Schema
-------------------

To get started, let's set up a new schema in MySQL Workbench and call it ``garden``.
In the last chapter, we learned we can do this by clicking on *New Schema*, naming it ``garden``, accepting the defaults, and clicking *Apply*.

Import New Tables
-----------------

To import the data in our CSVs, we need to create three empty tables.

Our first table is ``plant``. ``plant`` needs to have four columns:

#. ``plant_id``, which will be the primary key for our database.
#. ``plant_name``, which will contain the name of the plant.
#. ``zone`` is an integer for the hardiness zone that our plant will live in best.
#. ``season`` is either ``"Winter"``, ``"Spring"``, ``"Summer"``, or ``"Fall"`` depending on which season our plant blooms in.

In a new query tab, use ``CREATE TABLE`` to make the ``plant`` table.
After you have created the ``plant`` table, you need to import some data.

Our second table is ``seeds``. ``seeds`` needs to have five columns:

#. ``seed_id``, which will auto increment.
#. ``expiration_date``, which will be of the ``DATE`` type.
#. ``quantity`` is an integer for the number of seeds we have available.
#. ``reorder`` of type ``BOOL`` and tells us if we need to reorder that type of seed.
#. ``plant_id`` is the foreign key that connects ``seeds`` to ``plant``.

In a new query tab, use ``CREATE TABLE`` to make the ``seeds`` table.
After you have created the ``seeds`` table, you need to import some data.

Our third table is ``garden_bed``. ``garden_bed`` needs to have four columns:

#. ``space_number``, which will increment as we plant new plants.
#. ``date_planted`` of type ``DATE`` for the date we planted that plant on.
#. ``doing_well`` of type ``BOOL`` and tells us if the plant is doing well.
#. ``plant_id`` is the foreign key that connects ``garden_bed`` to ``plant``.

In a new query tab, use ``CREATE TABLE`` to make the ``garden_bed`` table.
After you have created the ``garden_bed`` table, you need to import some data.

Try out some joins!
-------------------

Before we jump in with our subqueries and more complex queries, let's practice our joins from the previous chapter.
After you write each query, look at the result set and reflect on why that information might be helpful.
If you needed this database to manage your own garden, what would you use the result set for?

Inner Join
^^^^^^^^^^

Write a query that joins ``seeds`` and ``garden_bed`` with an inner join to see what plants are we have seeds for that are *also* planted in the garden bed.

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

When we were writing our joins, you may have noticed that the information that was most helpful to you (the ``plant_name``) was missing from the result set!

Write a query that gets the name of the plant by joining the ``plant`` table on the result set of the inner join query above.

Let's say our ``plant`` table is so large that we have no idea what the ``plant_id`` for a hosta is. All we know is that there is definitely a row for hostas in the ``plant`` table.

Write a query that will insert a new row into our ``seeds`` table. This new row needs to show that we received 100 hosta seeds that will expire on 08/05/2020 (so no need to reorder!) and for the ``plant_id``, use a query *inside* the INSERT statement to get the appropriate ID for hostas.

Bonus Missions
--------------

#. Revisit your query with a full join and try using ``UNION ALL`` as opposed to ``UNION``. How does the result set differ?
#. Now that we can get the ``plant_name`` of plants that we have seeds for and are in the garden bed, try using ``COUNT()`` to see how many plants are in both places.


