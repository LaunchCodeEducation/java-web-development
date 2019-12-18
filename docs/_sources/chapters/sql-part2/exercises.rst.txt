Exercises: SQL, Part 2
=======================

Start up MySQL Workbench and select your ``practiceDB`` from the previous chapter.

We are going to add to our garden database to practice our new SQL skills.

Import New Tables
-----------------

In addition to the ``seeds`` table, we need to add a ``plant`` table and a ``garden_bed`` table.

Our ``plant`` table needs to have ``plant_id`` column, a ``name`` column, a ``zone`` column, and a ``season`` column.

Our ``garden_bed`` table needs to have a ``plant_id`` column, a ``date`` column, and a ``doing_well`` column.

We also need to modify our seeds table to include the ``plant_id`` column.

``plant_id`` is going to be our foreign key that will connect ``plant`` to `` seed`` and ``garden_bed``.

Inner Join
----------

Inner join ``seeds`` and ``garden_bed`` to see what plants are we have seeds for and are also planted.

Why is this helpful?

Left Join
---------

Left join to see all of the seeds and corresponding planted plants.

Why is this helpful?

Right Join
----------

Right join to see all of the seeds and corresponding planted plants.

Why is this helpful?

Full Join
---------

Instructions for 2 full joins:

#. seeds and garden_bed. Does this match all that is in plants?

Sub-Queries
-----------

