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

Code along with the following examples using the ``storage`` database and
tables you created earlier.

Inner Join
^^^^^^^^^^

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

   .. figure:: ./figures/inner-join-result-set.png
      :alt: Result set for an inner join of the writing_supply and pencil_drawer tables.

   We could accomplish the same result using a series of simple queries, but
   this would be inefficient. We would need to first run a query on
   ``writing_supply`` and then use the results to shape one or more queries on
   ``pencil_drawer``.

To reduce the size of the result set, we can request specific fields and add
conditions to the query:

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, pencil_type, drawer_id, quantity
      FROM writing_supply
      INNER JOIN pencil_drawer ON writing_supply.supply_id = pencil_drawer.supply_id
      WHERE refill = true AND pencil_type = "Mechanical";

   **Result Set**

   .. figure:: ./figures/inner-join-with-conditions.png
      :alt: Result set for an inner join with a WHERE clause.

   Note that in line 1, we need to specify the source for ``supply_id``, since
   both tables contain a column with that name.

Left/Right Join
^^^^^^^^^^^^^^^^

We can use a ``LEFT`` or ``RIGHT`` join to retain all of the records from one
table and pull in overlapping data from another.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, utensil_type, drawer_id, color
      FROM writing_supply
      LEFT JOIN pen_drawer ON writing_supply.supply_id = pen_drawer.supply_id;

   The result set contains ``null`` values for any rows that involve pencils. The
   left join retains all of the data in ``writing_supply``, but it can only
   combine that information with data from ``pen_drawer`` if the rows share
   ``supply_id`` values.

   .. figure:: ./figures/left-join-result-set.png
      :alt: Result set for an inner join with a WHERE clause.

As with inner joins, we can restrict the size of the result set by adding one
or more conditions:

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, utensil_type, drawer_id, color, quantity
      FROM writing_supply
      LEFT JOIN pen_drawer ON writing_supply.supply_id = pen_drawer.supply_id
      WHERE refill = true;

   **Result Set**

   .. figure:: ./figures/left-join-with-condition.png
      :alt: Result set for a left join with a WHERE clause.

Multiple Joins
^^^^^^^^^^^^^^

The ``UNION`` keyword allows us to combine the results of separate ``SELECT``
commands. Run each of the following queries individually and examine the two
result sets. Next, run the queries with ``UNION``.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT writing_supply.supply_id, utensil_type, drawer_id, quantity FROM writing_supply
      LEFT JOIN pencil_drawer ON writing_supply.supply_id = pencil_drawer.supply_id
      WHERE refill = true

      UNION

      SELECT writing_supply.supply_id, utensil_type, drawer_id, quantity FROM writing_supply
      RIGHT JOIN pen_drawer ON writing_supply.supply_id = pen_drawer.supply_id
      WHERE refill = true
      ORDER BY supply_id;

   **Result Set**

   .. figure:: ./figures/union-of-two-joins.png
      :alt: Result set for UNION of a left and right join.

Lines 1 - 3 merge data from ``pencil_drawer`` into ``writing_supply``, so long
as the rows have matching ``supply_id`` values and have ``refill`` set as
``true``. Lines 7 - 10 merge data from ``writing_supply`` into ``pen_drawer``
with the same conditions. The ``UNION`` command combines the two result sets.

.. admonition:: Note

   Recall that MySQL has no ``FULL OUTER JOIN`` syntax. If we want to combine
   all of the data from two separate tables, we must use the ``UNION``
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
      /* First result set contains the supply_id values 1, 2, and 5. */

      SELECT drawer_id, color FROM pen_drawer
      WHERE quantity >= 60 AND supply_id = 5;

   **Second Result Set**

   .. figure:: ./figures/two-simple-queries.png
      :alt: Result set of the two simple SQL queries.

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

   **Result Set**

   .. figure:: ./figures/all-pen-drawers.png
      :alt: Result set of the initial complex SQL query.

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
returns values for ALL drawers in ALL of the pen supply containers. Let's
modify the query by adding the condition for ``quantity``.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      SELECT drawer_id, color FROM pen_drawer
      WHERE supply_id IN (SELECT supply_id FROM writing_supply WHERE utensil_type = "Pen")
      AND quantity >= 60;

   **Result Set**

   .. figure:: ./figures/over60-pen-drawers.png
      :alt: Result set of the restricted complex SQL query.

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

   **Result Set**

   .. figure:: ./figures/two-simple-queries.png
      :alt: Result set of the final, complex SQL query.

Success! Our complex SQL query now produces the same result as the two
separate, simple SQL queries. However, using a subquery is more flexible, since
it does not rely on hard-coded values. We can see this benefit if we add 100
more entries to ``writing_supply``. The original pair of queries still checks
for entries with ``supply_id = 5``, even though this may no longer be the last
pen container. The complex query correctly identifies the last pen container
regardless of how many entries ``writing_supply`` contains.

Where Else Can We Add Subqueries?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the examples above, you added one subquery into the ``WHERE`` clause of
another SQL command. However, it is also possible to place a subquery in the
``FROM`` clause. Instead of pulling values from an entire table, this
setup retrieves data from the result set of the inner query.

Subqueries can be used with ``INSERT``, ``UPDATE``, and ``DELETE`` commands,
and it is also possible to place subqueries inside subqueries. We will not go
over these options here, but the links below provide some examples if you wish
to explore the topics on your own:

#. `Subquery with INSERT <https://www.w3schools.com/sql/sql_insert_into_select.asp>`__,
#. `Subquery with UPDATE or DELETE <https://www.w3resource.com/sql/subqueries/understanding-sql-subqueries.php>`__,
#. `Nested subqueries <https://www.w3resource.com/sql/subqueries/nested-subqueries.php>`__.

Last Reminders
^^^^^^^^^^^^^^

#. In most cases, subqueries should be enclosed in parentheses ``()``.
#. If a subquery returns multiple rows in its result set, using the comparison
   operators (``=``, ``>``, ``<=``, etc.) in a ``WHERE`` clause throws an
   error. In these cases, use ``ANY``, ``ALL``, or ``IN`` to check the
   condition across all of the rows.
#. In a ``WHERE`` clause, a subquery must be placed on the *right hand side* of
   the comparison operator (``ANY``, ``IN``, ``=``, ``>``, etc.)

Check Your Understanding
-------------------------

.. admonition:: Question

   ``UNION`` and ``JOIN`` produce the same result set.

   a. True
   b. False

.. Answer = False

.. admonition:: Question

   A subquery and a ``UNION`` accomplish the same thing.

   a. True
   b. False

.. Answer = False

.. admonition:: Question

   What is the execution order for the following complex SQL query?

   .. sourcecode:: SQL
      :linenos:

      SELECT column_1 FROM table_1
      WHERE column_1 IN (SELECT column_2 FROM table_2
         WHERE column_2 IN (SELECT column_3 FROM table_3
            WHERE num_items > 30));

   a. ``SELECT column_1``, then ``SELECT column_2``, then ``SELECT column_3``
   b. ``SELECT column_1``, then ``SELECT column_3``, then ``SELECT column_2``
   c. ``SELECT column_2``, then ``SELECT column_1``, then ``SELECT column_3``
   d. ``SELECT column_2``, then ``SELECT column_3``, then ``SELECT column_1``
   e. ``SELECT column_3``, then ``SELECT column_1``, then ``SELECT column_2``
   f. ``SELECT column_3``, then ``SELECT column_2``, then ``SELECT column_1``

.. Answer = f (3, then 2, then 1)
