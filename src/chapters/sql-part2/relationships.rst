Table Relationships
===================

As mentioned briefly in the last chapter, we want to keep the design of our
database tables *clean*. Each table should deal with a very narrow set of data,
and any specific piece of information should be stored in ONLY ONE PLACE. This
makes it much simpler to perform updates, since changes can be applied once
rather than over multiple tables.

For example, a school might keep track of their course offerings by creating a
``courses`` table. This would include information such as an ID number, title,
duration, a short description, and number of credits. All of these items define
a course---Chemistry, for example.

Every course has an assigned teacher as well as a student roster, and these may
also seem like good things to add to the ``courses`` table. However, a list of
student names does NOT define "Chemistry". Since student placement in a
course is temporary, the roster data needs to be kept in a separate location.
Similarly, multiple teachers could run the same course. Since there could be
two Chemistry classes that take place during 1st period, the names of
specific instructors should be kept out of the ``courses`` table.

A separate ``teachers`` table would include information like ID, name, email,
and hire date---everything the school needs to define an instructor. Data such
as courses taught, planning period, or room number would NOT go into this
table, since these items can change every year and are not specific to one
person.

Similarly, a ``students`` table could contain ID, name, email, courses
completed, parent phone numbers, and grades---anything that defines a
particular child. Something like the name of their first period teacher would
be stored elsewhere.

So, ``courses`` only holds data that directly defines each class the school
offers. ``teachers`` only contains information that defines each instructor,
and ``students`` stores student data and nothing else. This sounds obvious, but
it is very easy to throw lots of data into a table and provide descriptive
column names. While this may seem like a good idea at the time, it leads to
repetition of data, and it makes maintaining that information more difficult.

Any time you add a new column to a table, ask yourself whether the data it
represents *defines* that table. If you answer *No*, then store the data in
a different place (e.g. ``lunch_period`` does not fit within ``students``, so
it will have to go in a different table, such as ``schedule``).

Relating Data
-------------

Keeping data in separate, smaller chunks is more efficient than keeping a huge
amount of data in one place. However, this often means we need to access
information stored in different tables. To gather all the data we want, we will
have to combine parts of these tables to get the whole picture.

For our school example, knowing which students are enrolled in which classes is
useful. Similarly, we might want to display a list of students shared by a
group of teachers.

*Relational databases* allow us to link tables together. Even though teacher
names are not stored in ``courses``, a connection can be made between that
table and ``teachers``.

Inside ``courses`` we can add an ``instructor`` column. However, this column
will NOT hold any names. Instead, it will store references that point to the
``teachers`` table. These references identify the information in ``teachers``
that is connected to a particular entry in ``courses``.

.. _one-to-many-sql:

One-To-Many Relationships
--------------------------

.. index:: ! one-to-many relationship

A common structure for database tables is the **one-to-many relationship**.
In this form, each entry in one table relates to many rows in a different
table. For example, a single row in ``courses`` represents one class offered by
a school. That single course can be taught by multiple teachers, and lots of
different students will be enrolled in it. Thus, *one* entry in the ``courses``
table relates *to many* entries in ``teachers`` and ``students``.

.. admonition:: Note

   For another example of the one-to-many concept, feel free to read
   `this article <http://www.databaseprimer.com/pages/relationship_1tox/>`__.

Table Keys
----------

To connect the ``courses`` table to ``teachers`` in a one-to-many relationship,
the following conditions must be met:

.. index:: ! primary key, ! foreign key

#. Each table must include a **primary key** column. A primary key is a unique,
   numerical identifier given to an entry.
#. The ``teachers`` table must include a **foreign key** column. Foreign keys
   are integers that tie directly to the entries in a different table. In our
   school example, the foreign key for a row in ``teachers`` matches one
   primary key in ``courses``.

Note that different teacher entries could have the same value for the foreign
key. This sets up the one-to-many link between a single row in ``courses`` and
multiple rows in ``teachers``.

Adding a Primary Key
^^^^^^^^^^^^^^^^^^^^

In MySQL, the syntax for creating a primary key column is:

.. sourcecode:: SQL

   column_name INTEGER PRIMARY KEY AUTO_INCREMENT

``column_name`` usually involves the term "id", and ``AUTO_INCREMENT``
ensures that each entry gets assigned a different integer value.

For our school example, the code to create ``courses`` could look like:

.. sourcecode:: SQL
   :linenos:

   CREATE TABLE courses (
      course_id INTEGER PRIMARY KEY AUTO_INCREMENT,
      course_title VARCHAR(40),
      course_minutes INTEGER,
      course_description TEXT,
      credits INTEGER
   );

Adding a Foreign Key
^^^^^^^^^^^^^^^^^^^^

The general syntax for creating a foreign key column is:

.. sourcecode:: SQL
   :linenos:

   column_name INTEGER,
   FOREIGN KEY (column_name) REFERENCES other_table(primary_key_column)

Line 2 establishes the relationship between two tables. One way to interpret
the line is, *The value for 'column_name' in this table relates to the entry in
'other_table' that has a matching primary key*.

For our school example, the code to create ``teachers`` could look like:

.. sourcecode:: SQL
   :linenos:

   CREATE TABLE teachers (
      teacher_id INTEGER PRIMARY KEY AUTO_INCREMENT,
      first_name VARCHAR(40),
      last_name VARCHAR(40),
      email VARCHAR(80),
      hire_date DATE,
      course_id INTEGER,
      FOREIGN KEY (course_id) REFERENCES courses(course_id)
   );

Note that in line 7, the name given to the foreign key column in ``teachers``
matches the name of the primary key column in ``courses``. Following this
convention helps you keep the relationships between your tables clear.

.. admonition:: Note

   In the :ref:`last studio <movie-sqls>`, you established a relationship
   between a ``directors`` table and a ``movies`` table using a foreign key.

Keys Wrap-Up
^^^^^^^^^^^^

#. Define a primary key column for each table in the database.
#. Define a foreign key column for any table that fulfills the *many* role of a
   one-to-many relationship.
#. The foreign key of the *many* relates to the primary key of the *one*.

.. admonition:: Tip

   Even if you do not think a table needs one, define a primary key column
   anyway. Your database needs to grow and adapt to change. Adding a primary
   key column to a table at the beginning helps with that.

Other Relationships
-------------------

Besides the common one-to-many structure, there are two other ways to relate
tables to each other. Read the following articles (or do a quick Google search)
to explore these options:

#. `One-to-one <http://www.databaseprimer.com/pages/relationship_1to1/>`__
#. `Many-to-many <http://www.databaseprimer.com/pages/relationship_xtox/>`__

You will need this information to answer the last few concept check questions.

Check Your Understanding
-------------------------

.. admonition:: Question

   Which if the following is the BEST table to store the period and room number
   for an Algebra I course?

   a. ``teachers``
   b. ``students``
   c. ``courses``
   d. ``schedule``

.. Answer = d (schedule)

.. admonition:: Question

   Which type of relationship exists between a ``dresser`` table and a
   ``drawer`` table?

   a. One-to-one
   b. One-to-many
   c. Many-to-many

.. Answer = b (one-to-many)

.. admonition:: Question

   Which type of relationship would exist between the ``teachers`` and
   ``students`` tables?

   a. One-to-one
   b. One-to-many
   c. Many-to-many

.. Answer = c (many-to-many)

.. admonition:: Question

   For the ``closet``, ``shelf``, and ``box`` tables, what are the
   relationships? (Don't overthink this).

   a. One-to-many and one-to-many
   b. One-too-many questions
   c. Many-too-many-too-many questions
   d. Um, wait, but... NOOOOOOO! I overthought it!

.. Answer = a (one-to-many and one-to-many)
