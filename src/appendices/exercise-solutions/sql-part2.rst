.. _sql-part2-exercise-solutions:

Exercise Solutions: The SQL Sequel
==================================

Try Out Some Joins!
-------------------

Before we jump in with our subqueries and more complex queries, let's practice our joins from the previous chapter.
After you write each query, look at the result set and reflect on why that information might be helpful.
If you needed this database to manage your own garden, how would you use the result set?

.. _sql-part2-exercise-solutions-inner-join:

Inner Join
^^^^^^^^^^

Use an inner join on ``seeds`` and ``garden_bed`` to see which plants we have seeds for and are in our garden bed.

.. sourcecode:: sql

   SELECT * 
   FROM seeds
   INNER JOIN garden_bed ON (seeds.plant_id=garden_bed.plant_id);

:ref:`Back to the exercises <sql-part2-exercises>`

.. _sql-part2-exercise-solutions-right-join:

Right Join
^^^^^^^^^^

Write a query that joins ``seeds`` and ``garden_bed`` with a right join to see all the plants in the garden bed and any matching seeds we have.

.. sourcecode:: sql

   SELECT *
   FROM seeds
   RIGHT JOIN garden_bed ON seeds.plant_id=garden_bed.plant_id;

:ref:`Back to the exercises <sql-part2-exercises>`

.. _sql-part2-exercise-solutions-sub-query:

Sub-Queries and Complex Queries
-------------------------------

#. When we were writing our joins, you may have noticed that the information that was most helpful to you (the ``plant_name``) was missing from the result set! Write a query that gets the name of the plant by joining the ``plant`` table on the result set of the inner join query above. *Hint*: Open the query tab with the inner join query and copy it into a new query tab to start. Once you have your inner join setup in a new query tab, it will be easier to write your subquery.

.. sourcecode:: sql
   :linenos:

   SELECT plant_name 
   FROM plant
   INNER JOIN 
	   (SELECT seeds.plant_id FROM seeds INNER JOIN garden_bed ON seeds.plant_id=garden_bed.plant_id) AS planted_plants ON plant.plant_id=planted_plants.plant_id;

:ref:`Back to the exercises <sql-part2-exercises>`