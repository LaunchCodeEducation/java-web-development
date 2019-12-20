Studio: Library
===============

Word has gotten out about your amazing SQL skills!
The head librarian at the local library asked if you could help with their database.

Database Setup
--------------

Let's start by creating a new schema in MySQL Workbench called ``library``.
Once you have accepted all defaults and hit "Apply", run the provided scripts to create tables and add data.
By the end of your setup, you should have 6 tables:

#. ``book``
#. ``author``
#. ``patron``
#. ``reference_book``
#. ``genre`` 
#. ``loan``

Loan Out a Book
---------------

A big function that you need to implement for the library is a query that updates the database when a book is loaned out.

The query needs to perform the following functions:

#. Change ``available`` to ``FALSE`` for the appropriate book.
#. Add a new row to the ``loan`` table with today's date as the date out and the ids in the row need to match the appropriate ``patron_id`` and ``book_id``.
#. Update the appropriate ``patron`` with the ``loan_id`` for the new row created in the ``loan`` table.

You can use any patron and book that strikes your fancy to create this query!

Check a Book Back In
--------------------

Working with the same patron and book, create the new query!

The other key function that we need to implement is checking a book back in.
To do so, the query needs to:

#. Change ``available`` to ``TRUE`` for the appropriate book.
#. Update the appropriate row in the ``loan`` table with today's date as the date in.
#. Update the appropriate ``patron`` changing ``loan_id`` back to ``null``.

Queries
-------

Write the following 3 queries to get warmed up.

#. Return the reference book titles and their ISBNs.
#. Return all of the books written by authors who are currently still living.
#. Return the names of the patrons with the genre of every book they currently have checked out.

Bonus Mission
-------------

#. Return the counts of the books of each genre.
#. A reference book cannot leave the library. How would you modify either the ``reference_book`` table or the book table to make sure that doesn't happen? Try to apply your modifications.
