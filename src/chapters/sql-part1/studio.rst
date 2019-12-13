Studio: Databases Part 1
=========================

A database fills the role of the model in an MVC structure.

In this studio, you will use space in *MySQLWorkbench* to practice writing SQL
queries to retrieve or modify information stored in an established database.
You will also explore the parallels between Java objects and database tables.

Walkthrough
------------

Let's relate what you've learned about SQL to interact with a database called
``movie-buff`` that contains two tables---``movies`` and ``directors``.

Just as you did in the :ref:`exercises <sql-part1-exercises>` create the new
``movie-buff`` schema.

Before we create the ``movies`` and ``directors`` tables, let's think about
what kind of columns we want in each one.

Movies Table
^^^^^^^^^^^^

For the ``movies`` table, it makes sense to have columns for the ``title`` of
the movie, the ``year`` it was released, and the ``director``. We're also going
to want to have a unique ``movie_id`` column as the primary key, since there
can be more than one movie with the same title.

Take the time now to think about what data types you might use for these
columns (``INTEGER``, ``VARCHAR``, ``DATE``, etc.), then go ahead and write (or
type) the SQL statement to create this table.

As you consider which data types to use for your ``movies`` columns, you might
find yourself thinking, *If this were a property of a Java object, what data
type would I use?*

For example, if the ``movie`` object has a ``title`` and a ``director`` field,
you would expect both of these data types to be ``String``. Similarly the year
the movie was released would be stored as an integer. This conceptual overlap
between databases and Java objects is very useful, and we will explore this
further in the class on *Object-Relational Mapping* (ORM).

Here's how our ``movies`` table could be created:

.. sourcecode:: sql
   :linenos:

   CREATE TABLE movies (
      movie_id INTEGER PRIMARY KEY AUTO_INCREMENT,
      title VARCHAR(120),
      year INTEGER,
      director VARCHAR(80)
   );

(Take a moment to discuss with a partner why the two ``VARCHAR`` parameters
differ).

Directors Table
^^^^^^^^^^^^^^^

Next, let's consider the properties we'd want for a ``director`` object in
Java. These could include a ``first`` name, a ``last`` name, and maybe the
``country`` where the director was born.

Once we identify the data types for these properties, we can write the SQL
command to create the ``directors`` table. Also, we should include a
``director_id`` column in order to create a valid primary key.

.. _directors-table:

.. sourcecode:: sql
   :linenos:

   CREATE TABLE directors (
      director_id INTEGER PRIMARY KEY AUTO_INCREMENT,
      first VARCHAR(40),
      last VARCHAR(40),
      country VARCHAR(80)
   );

Relating the Tables
^^^^^^^^^^^^^^^^^^^^

Before we go further, let's take a moment to think about how these two tables
relate to each other, and whether we may want to modify the column ``director``
in the ``movies`` table. Understanding the common *one-to-many* relationship
that exists between database tables helps us set up the best design for
``movies`` and ``directors``. A director can work on multiple movies, but each
movie may only have one director.

.. admonition:: Note

   It may be useful to review `this article <http://www.databaseprimer.com/pages/relationship_1tox/>`__
   to refresh your memory on the one-to-many concept.

In order to reflect a one-to-many relationship in the table definitions, let's
modify the ``director`` column in ``movies`` to become ``director_id``. It
should therefore be an ``INTEGER`` instead of the ``VARCHAR`` we used earlier
when we thought the ``director`` column would hold the name of a person.

We also will want to make the ``director_id`` column in ``movies`` a
*foreign key*, so that it links directly to the ``director_id`` column in the
``directors`` table. Go ahead and write the SQL to drop the old ``movies``
table, and then write the SQL command to create a new table with these changes.

.. sourcecode:: sql
   :linenos:

   DROP TABLE movies;

   CREATE TABLE movies (
      movie_id INTEGER PRIMARY KEY AUTO_INCREMENT,
      title VARCHAR(120),
      year INTEGER,
      director_id INTEGER,
      FOREIGN KEY (director_id) REFERENCES directors(director_id)
   );

.. admonition:: Note

   If needed, here is a set of review articles:

   #. `SQL Drop Table <https://www.w3schools.com/sql/sql_drop_table.asp>`__,
   #. `SQL Create Table <https://www.w3schools.com/sql/sql_create_table.asp>`__,
   #. `SQL Foreign Key <https://www.w3schools.com/sql/sql_foreignkey.asp>`__.

   Follow the MySQL syntax instructions when there is a syntax variation
   between the major databases.

Setting up our two tables this way keeps our design *clean*. It puts data
specific to directors in the ``directors`` table, places data specific to each
movie in the ``movies`` table, and it provides a link between the two tables.

Data such as the director's country is NOT an attribute of a movie, so there is
no need to clutter a ``movie`` object or the ``movies`` table with that
information. Instead, a country name is an attribute of the director, so that
data should be stored in ``directors`` table.

However, we might want to know that information for a given movie (e.g. we may
want to find all the movies since 2010 that have French directors). So we need
a way to filter the movies based on attributes from ``directors``. Solving this
challenge is what relational databases are all about, and ``Foreign Keys``
offer the solution.

``INSERT`` Data From File
^^^^^^^^^^^^^^^^^^^^^^^^^^

Rather than adding entries line by line, you will use a prepared SQL file to
speed up the process.

#. Follow this link to the `movie-buff data <https://gist.github.com/jimflores5/5276e5cf15e19ae0923f809ee2367c7f>`__
   repository.
#. Click the *Download Zip* button to save a copy of the file to your machine.
#. Double-click the zip file icon to extract the ``movie-buff-data.sql`` file
   (it will be inside a folder).
#. In MySQLWorkbench, click the *Open SQL* button, and select the
   ``movie-buff-data.sql`` file.

   .. figure:: ./figures/openSQLFileButton.png
      :alt: Click "Open SQL" button.

#. Double-click the ``movie-buff`` schema, then click the leftmost lightning
   bolt icon to run the SQL script. This will populate the ``directors`` and
   ``movies`` tables.

   .. figure:: ./figures/runMovieBuffSql.png
      :alt: Click the leftmost lightning bolt icon.
      :scale: 80%

#. Confirm that the tables contain data by clicking on the table icon next to
   each name.

   .. figure:: ./figures/moviesTableCheck.png
      :alt: Select table contents button.

OK! Your model is ready to accept queries.

Your Assignment
---------------

For this studio, you'll practice writing SQL queries to perform various data
retrieval and manipulation tasks. You will be using the ``movies`` and
``directors`` tables described :ref:`above <directors-table>`, so if you still
need to ``CREATE`` them, please do so now.

Task List
^^^^^^^^^

Open up a new *Query* tab in MySQLWorkbench. In that tab, write the SQL
commands to carry out each of the queries described below. As you complete each
step, compare your SQL code and the output with a partner.

#. List just the titles of all the movies in the database.

#. List the title and year of each movie in the database in *DESCENDING* order
   of the year released.

#. Insert a new record into the ``directors`` table for Rob Reiner, an
   American film director.

   .. admonition:: Note

      Recall that the column for ``director_id`` is auto incremented, so you
      don't need to put in a value for that column.

#. List the ``last`` name and ``director_id`` for Rob Reiner.

#. Insert a new record into the ``movies`` table for *The Princess Bride*,
   which was released in 1987 and directed by Rob Reiner.

   .. admonition:: Note

      ``movie_id`` is also auto incremented, so you don't need to put in a
      value for that column. However, you *will* need to provide a value for
      the foreign key, ``director_id``, to link the movie to the proper
      director.

#. List all columns for all records of the ``directors`` table in ascending
   alphabetical order based on the director's country of origin.

#. List all columns for all records of the ``directors`` table in ascending
   alphabetical order first by the director's country of origin and then by
   the director's last name.

#. If you list all of the data from the ``movies`` table
   (``SELECT * FROM movies;``), you will see a column of director ID numbers.
   This data is not particularly helpful to a user, since they probably want to
   see the director names instead. Use an *inner join* in your SQL command to
   display a list of movie titles, years released, and director last names.

#. List all the movies in the database along with the first and last name of
   the director. Order the list alphabetically by the director's last name.

#. List the first and last name for the director of *The Incredibles*. You can
   do this with either a join or a ``WHERE`` command, but for this step please
   use ``WHERE``.

#. List the last name and country of origin for the director of *Roma*. You
   can do this using either a join or a ``WHERE`` command, but for this
   step please use a join.

   .. admonition:: Tip

      For more join practice, take advantage of these resources at W3 Schools:

      #. `Inner joins <https://www.w3schools.com/sql/sql_join_inner.asp>`__,
      #. `Joins <https://www.w3schools.com/sql/sql_join.asp>`__.

#. Delete a row from the ``movies`` table. What consequence does this have on
   ``directors``? List the contents of both tables to find out.

#. Delete one person from the ``directors`` table, then re-run your SQL command
   from step 8. What consequence results from trying to remove a director?

Bonus Missions
---------------

#. Note that SQL *aliases* give a table or column a temporary name. Assign
   aliases in at least 3 of the items above to make the columns names different
   and/or more readable in the output.
#. List all of the movies in the database directed by Peter Jackson.
#. a. `Add another column <https://www.w3schools.com/sql/sql_alter.asp>`__ to
   the ``movies`` table that holds the amount of money earned by each film.

   b. Use ``UPDATE`` to enter these values for each movie in the database.
   c. Generate a list that ranks the movie titles based on earnings.
   d. Generate a list that only shows films that earned above (or below) a
      certain amount.
