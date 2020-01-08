Studio: A Library
=================

Word has gotten out about your amazing SQL skills!
The head librarian at the local library asked if you could help with their database.

Database Setup
--------------

Let's start by creating a new schema in MySQL Workbench called ``library``.
Once you have accepted all defaults and hit *Apply*, you need to create tables and import data from CSVs or add data via SQL query.
By the end of your setup, you should have 6 tables:

#. ``book``
#. ``author``
#. ``patron``
#. ``reference_books``
#. ``genre`` 
#. ``loan``

.. admonition:: Note

   For the starter data, you need to use the same `Github repo <https://github.com/LaunchCodeEducation/java-web-development-starter-data>`_ as the exercises. The files you need are in ``lesson-15-studio``.

The ``book`` table
^^^^^^^^^^^^^^^^^^

To create the ``book`` table, you can use the following SQL query:

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE book (
      book_id INT AUTO_INCREMENT PRIMARY KEY,
      author_id INT,
      title VARCHAR(255),
      isbn INT,
      available BOOL,
      genre_id INT
   );

For the starter data, use the ``books.csv`` file to the fill the table.

The ``author`` table
^^^^^^^^^^^^^^^^^^^^

Use the following query to create the ``author`` table.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE author (
      author_id INT AUTO_INCREMENT PRIMARY KEY,
      first_name VARCHAR(255),
      last_name VARCHAR(255),
      birthday DATE,
      deathday DATE
   );

For the starter data, use the ``authors.csv`` file to fill the ``author`` table.

The ``patron`` table
^^^^^^^^^^^^^^^^^^^^

Use the following query to create the patron table.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE patron (
      patron_id INT AUTO_INCREMENT PRIMARY KEY,
      first_name VARCHAR(255),
      last_name VARCHAR(255),
      loan_id INT
   );

To fill the table, use the ``patrons.csv`` file.

The ``reference_books`` table
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use the following query to create the ``reference_books`` table.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE reference_books (
      reference_id INT AUTO_INCREMENT PRIMARY KEY,
      edition INT,
      book_id INT,
      FOREIGN KEY (book_id)
         REFERENCES book(book_id)
         ON UPDATE SET NULL
         ON DELETE SET NULL
   );

To fill the table, use the following query.

.. sourcecode:: mysql
   :linenos:

   INSERT INTO reference_books(edition, book_id)
   VALUE (5,32);

The ``genre`` table
^^^^^^^^^^^^^^^^^^^

Use the following query to create the ``genre`` table.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE genre (
      genre_id INT PRIMARY KEY,
      genres VARCHAR(100)
   );

Use the ``genres.csv`` file to fill the ``genre`` table.

The ``loan`` table
^^^^^^^^^^^^^^^^^^

Use the following query to create the ``loan`` table.

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE loan (
      loan_id INT AUTO_INCREMENT PRIMARY KEY,
      patron_id INT,
      date_out DATE,
      date_in DATE,
      book_id INT,
      FOREIGN KEY (book_id)
         REFERENCES book(book_id)
         ON UPDATE SET NULL
         ON DELETE SET NULL
   );

For now, the ``loan`` table can stay empty! We will add information to it in a bit!

Warm-up Queries
---------------

Write the following queries to get warmed up.

#. Return the mystery book titles and their ISBNs.
#. Return all of the titles and author's first and last names for books written by authors who are currently living.

Loan Out a Book
---------------

A big function that you need to implement for the library is a script that updates the database when a book is loaned out.

The script needs to perform the following functions:

#. Change ``available`` to ``FALSE`` for the appropriate book.
#. Add a new row to the ``loan`` table with today's date as the ``date_out`` and the ids in the row matching the appropriate ``patron_id`` and ``book_id``.
#. Update the appropriate ``patron`` with the ``loan_id`` for the new row created in the ``loan`` table.

You can use any patron and book that strikes your fancy to create this script!

Check a Book Back In
--------------------

Working with the same patron and book, create the new script!

The other key function that we need to implement is checking a book back in.
To do so, the script needs to:

#. Change ``available`` to ``TRUE`` for the appropriate book.
#. Update the appropriate row in the ``loan`` table with today's date as the ``date_in``.
#. Update the appropriate ``patron`` changing ``loan_id`` back to ``null``.

Once you have created these scripts, loan out 5 new books to 5 different patrons.

Wrap-up Query
-------------

Write a query to wrap up the studio. This query should return the names of the patrons with the genre of every book they currently have checked out.

Bonus Mission
-------------

#. Return the counts of the books of each genre. Check out the `documentation <https://dev.mysql.com/doc/refman/8.0/en/counting-rows.html>`_ to see how this could be done!
#. A reference book cannot leave the library. How would you modify either the ``reference_book`` table or the book table to make sure that doesn't happen? Try to apply your modifications.

