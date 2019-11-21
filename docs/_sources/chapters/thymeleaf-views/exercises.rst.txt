Exercises: Thymeleaf
=====================

In the chapter, we started working on an application for tracking various coding events around town.

Open up your ``codingevents`` project in IntelliJ.

#. In addition to names of events, we want to add descriptions as well.
   Use fragments to store the name and description of different coding events around town.
   Use ``th:replace`` in your main template to bring in the descriptions and names for each event.
#. Wrap your ``ul`` tag with a ``div`` tag.
   Use ``th:unless`` to insure that the list shows up when the list is full and not empty.
#. Put together the events and descriptions in a table as opposed to a unordered list.


