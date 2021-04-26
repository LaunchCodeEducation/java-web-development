.. _thymeleaf-views-exercise-solutions:

Exercise Solutions: Thymeleaf Views
===================================

Expanding our Events Schedule
-----------------------------

.. _thymeleaf-views-exercise-solutions1:

#. Comment out your previous code in the ``displayAllEvents`` method.

   .. sourcecode:: java

      //        List<String> events = new ArrayList<>();
      //        events.add("Code With Pride");
      //        events.add("Strange Loop");
      //        events.add("Apple WWDC");
      //        events.add("SpringOne Platform");
   
   :ref:`Back to the exercises <thymeleaf-views-exercises>`

.. _thymeleaf-views-exercise-solutions3:   

3. Fill your ``events`` HashMap with the names and descriptions of 3 coding
   events around town.

   .. sourcecode:: java

      events.put("Menteaship","A fun meetup for connecting with mentors");
      events.put("Code With Pride","A fun meetup sponsored by LaunchCode");
      events.put("Javascripty", "An imaginary meetup for Javascript developers");

   :ref:`Back to the exercises <thymeleaf-views-exercises>`

.. _thymeleaf-views-exercise-solutions5:

5. Use fragments to store the address of the new tech hub where all of the
   programmers are hanging out. Use ``th:replace`` in your main template to
   bring in the address as a third column in your table.
   You may need to create a new ``fragments.html``.

   .. sourcecode:: guess

      <td th:fragment="address">1234 5th Street</td>

   :ref:`Back to the exercises <thymeleaf-views-exercises>`