Joins
=====

.. index:: ! join

A **join** combines two tables into one result set.
We can use joins when we want to query two tables at the same time. 
Whenever we join two tables, we have to specify the condition upon which the tables need to be joined.

In SQL, there are four different types of joins:

#. Inner Join
#. Left Outer Join
#. Right Outer Join
#. Full Outer Join

No matter which join you are working with, the general syntax for the query looks like so:

.. sourcecode:: mysql
   :linenos:

   SELECT ColumnName1, ColumnName2, ....
   FROM TableA
   TYPEOFJOIN JOIN TableB ON TableA.ColumnName1 == TableB.ColumnName1;

In this general query, we specified what columns we want (or we could have used the ``*`` to read data from all columns).
We have also specified that ``TableA`` is the *left* table and that ``TableB`` is the *right* table.
On line 3, we need to include the type of join as part of our query with the ``JOIN`` keyword and the condition upon which we are joining the tables.
Our condition follows the ``ON`` keyword and tells MySQL what we believe to be matching records.
This may mean we want to join on matching customer ids or matching dollar amounts or matching dates depending on the tables we are working with and what questions we need to answer.

.. index:: ! inner join

Inner Join
----------

Joining two tables on an **inner join** produces a result set that only includes the values that match in both tables.

.. admonition:: Example

   If we use an inner join to combine ``JohnsonWedding`` and ``JohnsonVowRenewal`` in a query, we can see what guests are going to both the vow renewal and the wedding.

   .. sourcecode:: mysql

      SELECT LastName, FirstName
      FROM JohnsonVowRenewal
      INNER JOIN JohnsonWedding ON JohnsonVowRenewal.GuestID == JohnsonWedding.GuestID;

   This query will give us a result set of the first and last names of the guests from the ``JohnsonVowRenewal`` table that are also in the ``JohnsonWedding`` table.

   .. figure:: figures/innerjoin.png
      :alt: Venn diagram highlighting just the center where the two circles meet.

   The venn diagram above shows the result set highlighted in blue.

.. index:: ! left outer join

Left Outer Join
---------------

Joining two tables on a **left outer join** gives us a result set will include all values in the left table and any matching records from the right table.

.. admonition:: Example 

   If we use a left inner join to combine ``JohnsonWedding`` and ``JohnsonVowRenewal`` in a query, we can see what all of the guests that were invited to the wedding and any guests who were also invited to the vow renewal.

   .. sourcecode:: mysql

      SELECT LastName, FirstName
      FROM JohnsonWedding
      LEFT OUTER JOIN JohnsonVowRenewal ON JohnsonWedding.GuestID == JohnsonVowRenewal.GuestID;

   .. figure:: figures/leftouterjoin.png
      :alt: Venn diagram highlighting the center and entirety of left circle.

   The venn diagram above shows the result set highlighted in blue.

.. index:: ! right outer join

Right Outer Join
----------------

Joining two tables on a **right outer join** gives us a result set that includes all values in the right table and any matching records from the left table.

.. admonition:: Example 

   If we use a right inner join to combine ``JohnsonWedding`` and ``JohnsonVowRenewal`` in a query, we can see what all of the guests that were invited to the vow renewal and any guests who were also invited to the wedding.

   .. sourcecode:: mysql

      SELECT LastName, FirstName
      FROM JohnsonWedding
      RIGHT OUTER JOIN JohnsonVowRenewal ON JohnsonWedding.GuestID == JohnsonVowRenewal.GuestID;

   .. figure:: figures/rightouterjoin.png 
      :alt: Venn diagram highlighting the center and entirety of right circle.

   The venn diagram above shows the result set highlighted in blue.  

.. index:: ! full outer join

Full Outer Join
---------------

Joining two tables on a **full outer join** gives us a result set that includes all records from both tables. 
Full outer joins are important to SQL, but the syntax is not supported in MySQL.
Instead, to achieve a full outer join, you have to work with a left outer join and a right outer join.
To show what a full outer join looks like in other types of SQL, we have simulated some possible syntax below.

.. admonition:: Example

   Now that another event planner has joined Mary's company, to get all of the events run by the company in August, we can use a full outer join to combine ``MaryEvents`` and ``LeahEvents``.

   .. sourcecode:: mysql

      SELECT *
      FROM MaryEvents
      FULL OUTER JOIN LeahEvents ON MaryEvents.Month == LeahEvents.Month
      WHERE MaryEvents.Month == 08;

   .. figure:: figures/fullouterjoin.png
      :alt: Venn diagram with the entirety of both circles highlighted.

   The venn diagram above shows the result set highlighted in blue.

Check Your Understanding
------------------------

.. admonition:: Question

   True or false, an inner join gives all of the records in both tables

.. ans: false!

.. admonition:: Question

   What bugs are in this SQL query? Select all that apply.

   .. sourcecode:: mysql

      SELECT 
      FROM JohnsonVowRenewal
      OUTER JOIN JohnsonWeding ON JohnsonVowRenewal.GuestID == JohnsonWedding.GuestID

   a. Nothing specified after ``SELECT``.
   b. ``JohnsonVowRenewal`` is spelled wrong.
   c. The type of join is not specified.
   d. ``JohnsonWedding`` is spelled wrong.
   e. ``ON`` is in the wrong place.
   f. There isn't a semicolon on the end of the SQL query.

.. ans: a, c, d, f