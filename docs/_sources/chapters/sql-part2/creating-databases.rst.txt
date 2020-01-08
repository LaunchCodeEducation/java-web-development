Database Management
===================

Back in the :ref:`Database and SQL chapter exercises <sql-part1-exercises>`,
you created a new database in MySQL Workbench with one table, ``seeds``.

Let's go through the process again, but this time we will set up one-to-many
relationships between three tables---``writing_supply``, ``pencil_drawer``,
and ``pen_drawer``. You will soon use these tables to practice more complex SQL
queries.

.. _practice-setup:

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
^^^^^^^^^^^^^^^^^^

3. Each record in this table will have three fields:

   a. A primary key, ``supply_id``.
   #. A ``utensil_type``, which will be an ``ENUM`` ("Pencil" or "Pen"). Note
      the syntax for setting this up in line 3 of the example.
   #. An integer number of drawers, ``num_drawers``.

.. admonition:: Example

   .. sourcecode:: SQL
      :linenos:

      CREATE TABLE writing_supply (
         supply_id INTEGER PRIMARY KEY AUTO_INCREMENT,
         utensil_type ENUM ("Pencil", "Pen"),
         num_drawers INTEGER
      );

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

.. _table-import-data:

Import Data
-----------

.. admonition:: Note

   Whenever you import existing data into your empty tables, it is helpful to
   use the same column names as the external source.

#. Follow this link to the
   `java-web-development-starter-data <https://github.com/LaunchCodeEducation/java-web-development-starter-data.git>`__.
   Fork the repository and then clone it to your machine.
#. Unlike previous repositories, this one only holds folders of CSV data files.
   It does NOT contain executable code.
#. Pay attention to where you save the folder for this repository. In the
   following steps, you need to access the files inside
   ``lesson-15-reading-data``.

   .. figure:: ./figures/csv-data-file-tree.png
      :alt: Table Data Import Wizard menu option.

#. In MySQL Workbench, right-click on the ``writing_supply`` table. Select
   *Table Data Import Wizard*.

   .. figure:: ./figures/SQLWorkbenchImport.png
      :alt: Table Data Import Wizard menu option.

#. In the next panel, click the *Browse* button. Find and select the
   ``writing_supply.csv`` file. Click *Next*.

   .. figure:: ./figures/importCsvFile.png
      :alt: Select file path to csv file.

#. In the following panel, select the default option
   *Use existing table --> storage.writing_supply*, and click *Next*.
#. Once again, accept the default options for importing data into your table
   columns. Click *Next*.

   .. figure:: ./figures/importColumns.png
      :alt: Select columns to import.

#. Clicking *Next* again will import the data. Clicking *Finish* on the final
   panel returns you to the editor.
#. In the query tab, run ``SELECT * FROM writing_supply`` to confirm that 6
   entries now exist in the table.
#. Repeat the steps 4 - 9 for the ``pencil_drawer`` and ``pen_drawer`` tables.

Confirm that the ``pencil_drawer`` and ``pen_drawer`` tables hold 6 and 15
entries, respectively. You are now ready to practice more advanced SQL queries.

Import Troubleshooting
----------------------

Did something go wrong with your import? No worries---the process is not always
perfect, and errors occur more often than we would like. A few issues are just
random glitches, but most others involve syntax or selection mistakes.

Here are some common errors:

#. **Filename**: Make sure that each file ends with the ``.csv`` extension.
   Also, select the correct file to import into each table (e.g.
   ``pen_drawer.csv`` will not import into the ``writing_supply`` table).
#. **Mismatched data types**: MySQL Workbench will not complete an import if
   you define a table column as one data type, but the matching column in the
   ``.csv`` file contains a different data type. Check to make sure that your
   ``CREATE`` statements correctly define the data types described in the
   :ref:`Setup <practice-setup>` section.
#. **Import order**: For one-to-many relationships, the *one* table must be
   created before the *many*, and this idea also applies to filling the tables
   with data. ``pen_drawer`` and ``pencil_drawer`` both contain foreign keys
   that link to ``writing_supply``. Thus, you must import data into
   ``writing_supply`` FIRST, before attempting to add data to the other two
   tables.

.. admonition:: Note

   This is not an exhaustive list of everything that could go wrong with a data
   import. Be patient and persistent, and don't hesitate to consult the
   `MySQL Workbench documentation <https://dev.mysql.com/doc/workbench/en/>`__,
   Google, your TA, or your instructor.

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
