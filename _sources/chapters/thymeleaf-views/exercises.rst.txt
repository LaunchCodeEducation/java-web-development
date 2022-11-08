.. _thymeleaf-views-exercises:

Exercises: Thymeleaf Views
==========================

In the chapter, we started working on an application for tracking various
coding events around town.

Open up your ``coding-events`` project in IntelliJ.

Getting Started
---------------

From your own ``add-bootstrap`` branch, create and checkout a new branch called ``my-views-exercises-solution``.

.. admonition:: Note

   If you need to make sure your code matches ours to start, look at the 
   `add-bootstrap branch <https://github.com/LaunchCodeEducation/coding-events/tree/add-bootstrap>`__  on ``coding-events-demo``.

Now, let's add descriptions to our events!

Expanding our Events Schedule
-----------------------------

#. Comment out your previous code in the ``displayAllEvents`` method.

   :ref:`Check your solution <thymeleaf-views-exercise-solutions1>`

#. In the videos, we learned how to use templates to display the elements in a
   static list called ``events``. Let's make our ``events`` list a HashMap!
   This enables us to add descriptions to our events.
#. Fill your ``events`` HashMap with the names and descriptions of 3 coding
   events around town.

   :ref:`Check your solution <thymeleaf-views-exercise-solutions3>`

#. Using ``th:block`` and ``th:each``, put together the events and their
   descriptions in a table as opposed to an unordered list.
#. Use fragments to store the address of the new tech hub where all of the
   programmers are hanging out. Use ``th:replace`` in your main template to
   bring in the address as a third column in your table.
   You may need to create a new ``fragments.html``.

   :ref:`Check your solution <thymeleaf-views-exercise-solutions5>`

#. Add some CSS to style your table to make it easier to read and center it on
   the page. You may need to create a new ``styles.css`` as well. Make sure to
   connect ``styles.css`` to the appropriate template with ``th:href``.

Bonus Mission
-------------

Try to add one more column to the table with pictures for each coding event.
You need to use ``th:href`` to pull in pictures in the appropriate template.
