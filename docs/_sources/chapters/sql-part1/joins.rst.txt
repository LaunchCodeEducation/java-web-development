Joins
=====

A **join** combines two tables into one. We can use joins to pull results across two tables, which might prove helpful when reviewing the guests of the Johnsons.

In SQL, there are four different types of joins:

#. Inner Join
#. Left Outer Join
#. Right Outer Join
#. Full Outer Join

Inner Join
----------

If we join table ``A`` and table ``B`` on an inner join, our result set will include values that match in both tables.

Left Outer Join
---------------

If we join table ``A`` and table ``B`` on a left outer join, our result set will include all values in the left table and any matching records from the right table.

Right Outer Join
----------------

If we join table ``A`` and table ``B`` on a right outer join, our result set will include all values in the right table and any matching records from the left table.

Full Outer Join
---------------

If we join table ``A`` and table ``B`` on a full outer join, our result set will include all records from both tables

Using Joins in our Queries
--------------------------

If we want to pull together two tables with a join as part o a query, we can do so like this:

.. sourcecode:: mysql

   SELECT LastName, FirstName
   FROM JohnsonWedding2
   INNER JOIN JohnsonWedding ON JohnsonWedding2.GuestID == JohnsonWedding.GuestID;

Here we specify that we want to retrieve the first and last names of the guests from who are in both weddings.