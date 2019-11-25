Exercises: Thymeleaf
=====================

In the chapter, we started working on an application for tracking various
coding events around town.

Open up your ``coding-events`` project in IntelliJ.

#. In addition to names of events, we want to add descriptions as well.
   Use fragments to store the name and description of different coding events
   around town.
   Use ``th:replace`` in your main template to bring in the descriptions and
   names for each event in the list.
#. Using ``th:block`` and ``th:each``, put together the events and their
   descriptions in a table as opposed to an unordered list. If you need a quick
   reminder for how to use these commands, review the
   :ref:`Iteration in a Template section <thymeleaf-iteration>` .
#. Add some CSS to style your table to make it easier to read and center it on
   the page. We do have file for ``styles.css`` that you can add to. Make sure
   to connect ``styles.css`` to the appropriate template with ``th:src``.

Bonus Mission
-------------

Try to add one more column to the table with pictures for each coding event.
You need to use ``th:href`` to pull in pictures in the appropriate template.
