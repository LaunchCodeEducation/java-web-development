Exercises: Thymeleaf
=====================

In the chapter, we started working on an application for tracking various
coding events around town.

Open up your ``coding-events`` project in IntelliJ.

Getting Started
---------------

Checkout a new branch off of ``master`` called ``my-exercises-solution``.

Now for some Git magic! We are going to go back in time to when our templates
were still using data from a static event list.

#. Use the ``git log`` command. Go through the logs until you find the commit
   where you finished creating a static event list.

   .. admonition:: Note

      If you were not making commits after each video, that is fine. You can fork and clone this `repo <https://github.com/LaunchCodeEducation/coding-events>`_ to get started.

#. Use ``git reset --hard <commit>`` to go back to that moment.

.. admonition:: Warning

   Before you reset to an older commit, make sure you are on a separate branch!
   This will reset your repo to a previous state!

Now, let's add descriptions to our events!

Expanding our Events Schedule
-----------------------------

#. Comment out your previous code in the ``displayAllEvents`` method.
#. In the videos, we learned how to use templates to display the elements in a
   static list called ``events``. Let's make our ``events`` list a HashMap!
   This enables us to add descriptions to our events.
#. Fill your ``events`` HashMap with the names and descriptions of 3 coding
   events around town.
#. Using ``th:block`` and ``th:each``, put together the events and their
   descriptions in a table as opposed to an unordered list.
#. Use fragments to store the address of the new tech hub where all of the
   programmers are hanging out. Use ``th:replace`` in your main template to
   bring in the address as a third column in your table.
   You may need to create a new ``fragments.html``.
#. Add some CSS to style your table to make it easier to read and center it on
   the page. You may need to create a new ``styles.css`` as well. Make sure to
   connect ``styles.css`` to the appropriate template with ``th:href``.

Bonus Mission
-------------

Try to add one more column to the table with pictures for each coding event.
You need to use ``th:href`` to pull in pictures in the appropriate template.
