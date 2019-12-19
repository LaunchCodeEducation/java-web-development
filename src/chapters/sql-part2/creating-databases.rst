Creating a Database
===================

Back in the :ref:`Database and SQL chapter exercises <sql-part1-exercises>`,
you created a new database in MySQL Workbench with one table, ``seeds``.

Let's go through the process again, but this time we will set up one-to-many
relationships between three tables---``cabinet``, ``drawer``, and ``file``. You
will soon use these tables to practice more complex SQL queries.

Setup
-----

#. Open a connection in MySQL Workbench. Click *Create New Schema* and call the
   model ``storage``.
#. Click *Apply*, and accept all of the default options when prompted.

The relationships between the three tables follows a logical progression. Each
``cabinet`` record relates to several ``drawer`` entries, and each ``drawer``
record relates in turn to multiple ``file`` entries.

Each table will need a primary key column, and ``drawer`` and ``file`` will
require foreign key columns. In the query tab of MySQL Workbench, ``CREATE``
the tables as described below.

``cabinet``
^^^^^^^^^^^

3. Each record in this table will have 3 fields:

   a. A primary key, ``cabinet_id``.
   #. An integer number of drawers, ``num_drawers``.
   #. A boolean describing whether or not the storage case is ``full``.

``drawer``
^^^^^^^^^^

4. Each record in this table will have 5 fields:

   a. A primary key, ``drawer_id``.
   b. The number of files, ``num_files``.
   c. An maximum number of files, ``max_files``.
   d. A boolean describing whether or not a drawer is ``full``.
   e. A foreign key (``cabinet_id``) that connects ``drawer`` with ``cabinet``.

``file``
^^^^^^^^

5. Each record in this table will have 5 fields:

   a. A primary key, ``file_id``.
   b. A ``file_type``, which will be an ``ENUM`` ("Invoice", "Contract",
      "Proposal").
   c. A file size, ``num_pages``.
   d. A summary of each file, ``description``.
   e. A foreign key (``drawer_id``) that connects ``file`` with ``drawer``.

Insert Data
-----------

.. admonition:: Note

   Whenever you import existing data into your empty tables, it is critical that
   you use the same column names as the external source.

#. Follow this link to the practice data...

      TODO: Add link to gist with the ``INSERT`` statements.

#. As you did in the first :ref:`SQL studio <movie-sqls>`, download and extract
   the ``.sql`` file.
#. Open the file in MySQL Workbench, and run the code to populate the tables.
