Table Relationships
===================

Intro text...
(Explain how and why data is split into related tables).

One-To-Many Relationships
--------------------------

We're also going to want to have a unique `movie_id` column as
the primary key, since there can be more than one movie with the same title.

Also, be sure to have an `director_id`
column so that we have a valid primary key.

.. sourcecode:: sql
   :linenos:

   CREATE TABLE directors (
      director_id INTEGER PRIMARY KEY AUTO_INCREMENT,
      first VARCHAR(120),
      last VARCHAR(120),
      country VARCHAR(120)
   );

Before we go further, let's take a moment to think about how these two tables
relate to each other, and whether we may want to modify the column `director`
in the `movies` table. Understanding the one-to-many relationship that is
common among database tables will help us to come up with the best design for
these two tables. A director may direct multiple movies, but each movie may
only have one director. 

.. admonition:: Note

   It may be useful to review `this article <http://www.databaseprimer.com/pages/relationship_1tox/>`__
   from the class prep to refresh your memory on the one-to-many concept.


In order to reflect this relationship in the table definitions, let's modify
the `director` column in `movies` to become `director_id` and therefore to be
an `INTEGER` instead of a `VARCHAR` (as that is the type we used earlier when
we thought the director column would hold the name of a director). We also
will want to make the `director_id` column a foreign key, so that it links
directly to the `director_id` column of the `directors` table. Go ahead and
write the SQL to drop the `movies` table we had created, and then write the
SQL to create a new table with these changes.

This kind of table structure keeps our database clean. It keeps data specific
to directors in the `directors` table, and data specific to each movie in the
`movies` table and provides a link between the two tables. This is a "clean"
design, because data such as what country the director of a movie is from
isn't really an attribute of the movie, it's an attribute of the director.
After all, you wouldn't put `directors_country` as a property of a Python
`movie` object, would you? Hopefully not. :-)

Still, we may want to know that information for a given movie, e.g., we may
want to find all the movies since 2010 that have French directors. So we need
to have a way of filtering movies based on attributes of directors, without
cluttering up the `movies` table. Solving this challenge is what relational
databases are all about, and Foreign Keys are the "key" (pun intended) to the
solution.

Foreign Keys
------------

Lorem ipsum...
