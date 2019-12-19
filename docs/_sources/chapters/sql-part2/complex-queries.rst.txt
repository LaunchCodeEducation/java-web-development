Complex Queries
===============

*Simple* SQL queries are commands that focus on only one parameter. These
include using the ``SELECT`` and ``WHERE`` keywords to perform straightforward
data retrieval. Simple queries usually collect data from only one table at a
time, and they narrow the result set with fairly simple conditions.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT *
      FROM movies
      WHERE release_date >= 2015;

   Note that in line 1, we selected all of the fields in the ``movies`` table,
   but we could easily replace ``*`` with a smaller set of column names.

*Complex* SQL queries go beyond the standard requests by retrieving data from
several tables and by limiting the result set with multiple conditions.

In the :ref:`previous chapter <sql-part1>`, you learned how to use joins to
display data that is spread over different tables. Another advanced SQL tool is
called a **subquery**, which is a simple SQL command embedded within another
query. By nesting queries, you can set up larger restrictions on the data
included in the result set.

Complex queries often combine joins and subqueries, and they may include
multiple ``AND``/``OR`` operators within the ``WHERE`` clause.

Review Joins
------------

Inner join example...

Left join example...

Right join example...

Full Outer Joins
^^^^^^^^^^^^^^^^

How to use ``UNION``...

Full outer join example.

Subqueries
----------

Consider:

#. Query for ids of cabinet with 3 or more drawers,
#. Query for ids of drawers with 50 or more files,
#. Query for ids of cabinets that have 3 or more drawers with 50 or more files.

SELECT cabinet_id FROM cabinet
WHERE num_drawers >= 3;

SELECT drawer_id FROM drawer
WHERE num_files >= 50;

SELECT cabinet_id, drawer_id
FROM cabinet
INNER JOIN drawers ON cabinet.cabinet_id = drawer.cabinet_id
WHERE num_drawers >= 3;

SELECT cabinet_id
FROM cabinet
INNER JOIN drawers ON cabinet.cabinet_id = drawer.cabinet_id
WHERE num_drawers >= 3
AND (SELECT drawer_id FROM drawer WHERE num_files >= 50);


Joins AND Subqueries
--------------------

Lorem ipsum...

Check Your Understanding
-------------------------

Lorem ipsum...
