Creating a Database
===================

Back in the :ref:`Database and SQL chapter exercises <sql-part1-exercises>`,
you created a new database in MySQL Workbench with one table, ``seeds``.

Let's go through the process again, but this time we will set up one-to-many
relationships between three tables---``writing_supply``, ``pencil_drawer``,
and ``pen_drawer``. You will soon use these tables to practice more complex SQL
queries.

Setup
-----

#. Open a connection in MySQL Workbench. Click *Create New Schema* and call the
   model ``storage``.
#. Click *Apply*, and accept all of the default options when prompted.

The three tables form a pair of one-to-many relationships. Each
``writing_supply`` record relates either to several ``pencil_drawer`` entries
or several ``pen_drawer`` entries.

Each table will need a primary key column, and ``pencil_drawer`` and
``pen_drawer`` will require foreign key columns. In the query tab of MySQL
Workbench, ``CREATE`` the tables as described below.

``writing_supply``
^^^^^^^^^^^^^^^^^^^

3. Each record in this table will have three fields:

   a. A primary key, ``supply_id``.
   #. A ``utensil_type``, which will be an ``ENUM`` ("Pencil" or "Pen").
   #. An integer number of drawers, ``num_drawers``.

``pencil_drawer``
^^^^^^^^^^^^^^^^^

4. Each record in this table will have five fields:

   a. A primary key, ``drawer_id``.
   b. The ``pencil_type``, which will be an ``ENUM`` ("Wood" or "Mechanical").
   c. An integer number of pencils, ``quantity``.
   d. A boolean describing whether or not it is time to ``refill`` the drawer.
   e. A foreign key (``supply_id``) that connects ``pencil_drawer`` with
      ``writing_supply``.

``pen_drawer``
^^^^^^^^^^^^^^

5. Each record in this table will have five fields:

   a. A primary key, ``drawer_id``.
   b. The ``color`` of the pens, which will be an ``ENUM`` ("Black", "Blue",
      "Red", "Green", "Purple").
   c. An integer number of pens, ``quantity``.
   d. A boolean describing whether or not it is time to ``refill`` the drawer.
   e. A foreign key (``supply_id``) that connects ``pen_drawer`` with
      ``writing_supply``.

Import Data
-----------

.. admonition:: Note

   Whenever you import existing data into your empty tables, it is helpful to
   use the same column names as the external source.

#. Follow this link to the
   `practice data <https://gist.github.com/jimflores5/d575333c633c194e0af13ed8e4ab4cdd>`__.
#. As you did in the first :ref:`SQL studio <movie-sqls>`, download the zip
   file. Double-click on it to extract three ``.csv`` files.
#. In MySQL Workbench, right-click on the ``writing_supply`` table. Select
   *Table Data Import Wizard*.

   .. figure:: ./figures/SQLWorkbenchImport.png
      :alt: Table Data Import Wizard menu option.

#. In the next panel, click the *Browse* button. Find and select the
   ``writing_supply.csv`` file. Click *Next*.

   .. figure:: ./figures/importCsvFile.png
      :alt: Select file path to csv file.

#. In the following panel, use the default option
   *Use existing table --> storage.writing_supply*, and click *Next*.
#. Once again, accept the default options for importing data into your table
   columns. Click *Next*.

   .. figure:: ./figures/importColumns.png
      :alt: Select columns to import.

#. Clicking *Next* again will import the data. Clicking *Finish* on the final
   panel returns you to the editor.
#. In the query tab, run ``SELECT * FROM writing_supply`` to confirm that 6
   entries now exist in the table.
#. Repeat the steps 3 - 8 for the ``pencil_drawer`` and ``pen_drawer`` tables.

Confirm that the ``pencil_drawer`` and ``pen_drawer`` tables hold 6 and 15
entries, respectively. You are now ready to practice more advanced SQL queries.

Check Your Understanding
------------------------

.. admonition:: Question

   Examine the setup you used for the ``writing_supply``, ``pencil_drawer``,
   and ``pen_drawer`` tables. Which of the following pairs does NOT have a
   one-to-many relationship?

   a. ``writing_supply`` and ``pencil_drawer``
   b. ``writing_supply`` and ``pen_drawer``
   c. ``pencil_drawer`` and ``pen_drawer``

.. Answer = c (``pencil_drawer`` and ``pen_drawer``)
