Creating a Database
===================

Back in the :ref:`Database and SQL chapter exercises <sql-part1-exercises>`,
you created a new database in MySQL Workbench with one table, ``seeds``.

Let's go through the process again, but this time we will set up one-to-many
relationships between three tables---``cabinet``, ``drawer``, and ``document``.
You will soon use these tables to practice more complex SQL queries.

Setup
-----

#. Open a connection in MySQL Workbench. Click *Create New Schema* and call the
   model ``storage``.
#. Click *Apply*, and accept all of the default options when prompted.

The relationships between the three tables follows a logical progression. Each
``cabinet`` record relates to several ``drawer`` entries, and each ``drawer``
record relates in turn to multiple ``document`` entries.

Each table will need a primary key column, and ``drawer`` and ``document`` will
require foreign key columns. In the query tab of MySQL Workbench, ``CREATE``
the tables as described below.

``cabinet``
^^^^^^^^^^^

3. Each record in this table will have 3 fields:

   a. A primary key, ``cabinet_id``.
   #. An integer number of drawers, ``num_drawers``.
   #. A boolean describing whether or not the storage case is ``is_full``.

``drawer``
^^^^^^^^^^

4. Each record in this table will have 4 fields:

   a. A primary key, ``drawer_id``.
   b. The number of files, ``num_files``.
   c. A boolean describing whether or not a drawer is ``is_full``.
   d. A foreign key (``cabinet_id``) that connects ``drawer`` with ``cabinet``.

``document``
^^^^^^^^^^^^

5. Each record in this table will have 5 fields:

   a. A primary key, ``document_id``.
   b. A ``document_type``, which will be an ``ENUM`` ("Invoice", "Contract",
      "Proposal").
   c. A document size, ``num_pages``.
   d. A summary of each document, ``summary``.
   e. A foreign key (``drawer_id``) that connects ``document`` with ``drawer``.

Insert Data
-----------

.. admonition:: Note

   Whenever you import existing data into your empty tables, it is helpful to
   use the same column names as the external source.

#. Follow this link to the
   `practice data <https://gist.github.com/jimflores5/d575333c633c194e0af13ed8e4ab4cdd>`__.
#. As you did in the first :ref:`SQL studio <movie-sqls>`, download the zip
   file. Double-click on it to extract three ``.csv`` files.
#. In MySQL Workbench, right-click on the ``cabinet`` table. Select *Table Data
   Import Wizard*.

   .. figure:: ./figures/SQLWorkbenchImport.png
      :alt: Table Data Import Wizard menu option.

#. In the next panel, click the *Browse* button. Find and select the
   ``cabinet.csv`` file. Click *Next*.

   .. figure:: ./figures/importCsvFile.png
      :alt: Select file path to csv file.

#. In the following panel, use the default option
   *Use existing table --> storage.cabinet*, and click *Next*.
#. Once again, accept the default options for importing data into your table
   columns. Click *Next*.

   .. figure:: ./figures/importColumns.png
      :alt: Select columns to import.

#. Clicking *Next* again will import the data. Clicking *Finish* on the final
   panel returns you to the editor.
#. In the query tab, run ``SELECT * FROM cabinet`` to confirm that 50 entries
   now exist in the table.
#. Repeat the steps 3 - 8 for the ``drawer`` and ``document`` tables.

Confirm that the ``drawer`` and ``document`` tables hold 200 and 1000 entries,
respectively. You are now ready to practice more advanced SQL queries.

Check Your Understanding
------------------------

.. admonition:: Question

   Examine the setup you used for the ``storage``, ``drawer``, and ``document``
   tables. Which of the following pairs does NOT have a
   one-to-many relationship?

   a. ``storage`` and ``drawer``
   b. ``storage`` and ``document``
   c. ``drawer`` and ``document``

.. Answer = b (``storage`` and ``document``)
