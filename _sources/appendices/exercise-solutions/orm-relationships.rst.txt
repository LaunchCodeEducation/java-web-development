.. _orm-relationships-exercise-solutions:

Exercise Solutions: The Early Bird gets the ORM!
================================================

Here is an example of how the README may turn out:

   1. Our ``Person`` class might hold the following fields:

      a. ``id`` (``int``) - the unique user ID

      b. ``firstName`` (``String``) - the user's first name

      c. ``lastName`` (``String``) - the user's last name

      d. ``email`` (``String``) - the user's email, which will also function as their username

      e. ``password`` (``String``) - the user's password

      The class would need getters for all of these fields. It could have setters for all fields except id (since it shouldn't change).

   2. The ``Person`` class might also have the following references:

      a. ``PersonProfile`` - a class to gather up all of the profile information about the user

      b. ``List<Events> eventsAttending`` - to store events the user wants to attend

      c. ``List<Events> eventsOwned`` - a different list, to store the events the user has created

   ``Person`` would have a many-to-many relationship with ``Event`` via ``List<Events> eventsAttending``.
   It would have a one-to-many relationship with ``Event`` via ``List<Events> eventsOwned``.

:ref:`Back to the exercises <orm-relationships-exercises>`