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
      INNER JOIN pencil_drawer ON writing_supply.supply_id = pencil_drawer.supply_id;

   The result set contains all of the records from both tables that have matching
   ``supply_id`` values.

   We could accomplish the same result using a series of simple queries, but
   this would be inefficient. We would need to first run a query on
   ``writing_supply`` and then use the results to shape one or more queries on
   ``pencil_drawer``.

To reduce the size of the result set, we can request specific fields and add
conditions to the query:

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, drawer_id, quantity
      FROM writing_supply
      INNER JOIN pencil_drawer ON writing_supply.supply_id = pencil_drawer.supply_id
      WHERE refill = true AND pencil_type = "Mechanical";

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

      SELECT writing_supply.supply_id, utensil_type, drawer_id, color
      FROM writing_supply
      LEFT JOIN pen_drawer ON writing_supply.supply_id == pen_drawer.supply_id;

   TODO: Add screenshot showing output.

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, utensil_type, drawer_id, color
      FROM writing_supply
      RIGHT JOIN pen_drawer ON writing_supply.supply_id == pen_drawer.supply_id;

   TODO: Add screenshot showing output.

As with inner joins, we can restrict the size of the result set:

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, utensil_type, drawer_id, color
      FROM writing_supply
      LEFT JOIN pen_drawer ON writing_supply.supply_id = pen_drawer.supply_id
      WHERE refill = true;

   TODO: Add screenshot showing output.

Multiple Joins
^^^^^^^^^^^^^^

The ``UNION`` keyword allows us to combine the result sets of separate join
commands.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, drawer_id, pencil_type, quantity FROM writing_supply
      LEFT JOIN pencil_drawer ON writing_supply.supply_id = pencil_drawer.supply_id

      UNION

      SELECT writing_supply.supply_id, drawer_id, color, quantity FROM writing_supply
      RIGHT JOIN pen_drawer ON writing_supply.supply_id = pen_drawer.supply_id;

   TODO: Add screenshot showing output.

Explanation of result set here...

.. admonition:: Note

   Recall that MySQL has no ``FULL OUTER JOIN`` syntax. If we want to combine
   all of the data from two separate tables, we would use the ``UNION``
   keyword between ``LEFT JOIN`` and ``RIGHT JOIN`` queries.

Subqueries
----------

Consider the following situations:

#. Retrieve the ``supply_id`` values for any ``writing_supply`` containers that
   hold pens.
#. Using the ``supply_id`` values, retrieve the ID and ``color`` values for
   any drawers in the last container that hold 60 or more pens.

We can accomplish these actions by using two simple SQL queries:

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT supply_id FROM writing_supply
      WHERE utensil_type = "Pen";
      /* Result set contains the supply_id values 1, 2, and 5. */

      SELECT drawer_id, color FROM pen_drawer
      WHERE quantity >= 60 AND supply_id = 5;

   TODO: Add screenshot of result set.

To complete the second SQL query, we must examine the result set from the
first, then hard-code the largest ``supply_id`` value into the line 6.
This is inefficient.

By using a subquery, we can combine the two SQL commands to accomplish the same
result. Let's begin by embedding one simple SQL command inside the ``WHERE``
clause of a second.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT drawer_id, color FROM pen_drawer
      WHERE supply_id IN (SELECT supply_id FROM writing_supply WHERE utensil_type = "Pen");

   TODO: Add screenshot of result set.

Items to note:

#. An embedded *inner query* will always execute before the *outer
   query*. In this case, the ``SELECT`` statement in line 2 runs first,
   followed by the ``SELECT`` statement in line 1.
#. The inner query in line 2 creates a result set of ``supply_id`` values from
   the ``writing_supply`` table, based on the condition
   ``utensil_type = "Pen"``.
#. The outer query returns a result set of ``drawer_id`` and ``color`` values
   from the ``pen_drawer`` table.
#. The condition ``WHERE supply_id IN`` checks if the ``supply_id`` value for
   a ``pen_drawer`` row matches one of the ``supply_id`` values returned from
   the inner query.

The result set from this complex SQL command is not yet what we want, since it
returns values for ALL pen drawers in ALL of the supply containers. Let's
modify the query by adding the condition for ``quantity``.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT drawer_id, color FROM pen_drawer
      WHERE supply_id IN (SELECT supply_id FROM writing_supply WHERE utensil_type = "Pen")
      AND quantity >= 60;

   TODO: Add screenshot of result set.

Now the result set shows only the information for pen drawers with 60 or more
items. This is good but still not quite complete, since we only want data from
the *last* ``writing_supply`` row that contains pens. To fix this, we need to
restrict the inner query to that single ``supply_id`` value.

The last pen container in ``writing_supply`` will have the largest value for
``supply_id``. Fortunately, SQL has a defined function, ``MAX(column_name)``,
that returns the largest value in the specified column.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT drawer_id, color FROM pen_drawer
      WHERE supply_id = (SELECT MAX(supply_id) FROM writing_supply WHERE utensil_type = "Pen")
      AND quantity >= 60;

   TODO: Add screenshot of result set.

Success! Our complex SQL query now produces the same result as the two
separate, simple SQL queries. However, the former is more flexible, since it
does not rely on hard-coded values. Assume we add 100 more entries to
``writing_supply``. The original pair of queries still checks for entries with
``supply_id = 5``, even though this may no longer be the last pen container.
The combined query correctly identifies the last pen container regardless of
how many entries ``writing_supply`` contains.

Joins with Subqueries
---------------------

Lorem ipsum...

Check Your Understanding
-------------------------

Lorem ipsum...
