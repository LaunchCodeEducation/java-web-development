Complex Queries
===============

*Simple* SQL queries are commands that perform straightforward data retrieval,
usually from only one table at a time. Examples of these queries include using
the ``SELECT`` and ``WHERE`` keywords, and they narrow the result set by
focusing on a single parameter.

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

Complex queries often combine joins and subqueries, and they may also include
multiple ``AND``/``OR`` operators within the ``WHERE`` clause.

Review Joins
------------

Code along with the following examples. Use the ``writing_supply``,
``pencil_drawer``, and ``pen_drawer`` tables you created earlier.

Inner Join
^^^^^^^^^^^

Each record in ``writing_supply`` stores a ``utensil_type`` value. We could use
a simple query to filter the records by type, but this would not contain data
such as ``quantity``, which is stored in a different table.

To return a result set that contains information that appears in both the
``writing_supply`` and ``pencil_drawer`` tables, we use an ``INNER JOIN``.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT *
      FROM writing_supply
      INNER JOIN pencil_drawer ON writing_supply.supply_id == pencil_drawer.supply_id;

   The result set contains all of the records from both tables that have matching
   ``supply_id`` values.

   We could accomplish the same result using a series of simple queries, but
   this would be inefficient. We would need to first run a query on
   ``writing_supply`` and then use the results to shape one or more queries on
   ``pencil_drawer``.

To restrict the size of the result set, we can request specific fields and add
conditions to the query:

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, drawer_id, quantity
      FROM writing_supply
      INNER JOIN pencil_drawer ON writing_supply.supply_id == pencil_drawer.supply_id
      WHERE refill == true AND type == "Wooden";

   Note that in line 1, we need to specify the source for ``supply_id``, since
   both tables contain a column with that name.

Left/Right Join
^^^^^^^^^^^^^^^^

We can use a ``LEFT`` or ``RIGHT`` join to retain all of the records from one
table and pull in overlapping data from another.

Let's compare the result of using a ``LEFT`` vs. ``RIGHT`` join on the
``writing_supply`` and ``pen_drawer`` tables.

.. admonition:: Examples

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, drawer_id, quantity
      FROM writing_supply
      LEFT JOIN pen_drawer ON writing_supply.supply_id == pen_drawer.supply_id;

   TODO: Add screenshot showing output.

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, drawer_id, quantity
      FROM writing_supply
      RIGHT JOIN pen_drawer ON writing_supply.supply_id == pen_drawer.supply_id;

   TODO: Add screenshot showing output.

As with inner joins, we can restrict the size of the result set:

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, drawer_id, color, quantity
      FROM writing_supply
      LEFT JOIN pen_drawer ON writing_supply.supply_id == pen_drawer.supply_id
      WHERE refill == true;

   TODO: Add screenshot showing output.

Full Outer Join
^^^^^^^^^^^^^^^^

Since MySQL has no ``FULL OUTER JOIN`` syntax, we use the ``UNION`` keyword to
combine the result sets of separate ``LEFT`` and ``RIGHT`` joins.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, drawer_id, color, quantity FROM writing_supply
      LEFT JOIN pen_drawer ON writing_supply.supply_id == pen_drawer.supply_id

      UNION

      SELECT writing_supply.supply_id, drawer_id, color, quantity FROM writing_supply
      RIGHT JOIN pen_drawer ON writing_supply.supply_id == pen_drawer.supply_id;

   TODO: Add screenshot showing output.

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
