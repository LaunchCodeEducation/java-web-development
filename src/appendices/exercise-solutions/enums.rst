.. _enums-exercise-solutions:

Exercise Solutions: Enum Practice
=================================

.. _enums-exercise-solutions5:

5. Before adding any other fields to ``Planets``, go to ``PlanetController``
   and update the index handler to pass in a ``Model`` class argument (eg. ``Model model``). 

   .. sourcecode:: java

      @GetMapping()
      public String displayIndex(Model model) {
         model.addAttribute("planets", Planets.values());
         return "index";
      }

   :ref:`Back to the exercises <enums-exercises>`

.. _enums-exercise-solutions7:

7. In ``templates/index``, create a list element and use the template
   variable you have just defined in the controller to list all of the 
   planet values on the page.

   .. sourcecode:: html

      <ol>
         <li th:each="planet : ${planets}" th:text="${planet}"></li>
      </ol>

   :ref:`Back to the exercises <enums-exercises>`

.. _enums-exercise-solutions9:

9. Update the template to display the planet names.

   .. sourcecode:: html

      <ol>
         <li th:each="planet : ${planets}" th:text="${planet.name}"></li>
      </ol>

   :ref:`Back to the exercises <enums-exercises>`

.. _enums-exercise-solutions11:

11. Change the index template to display a table of each planet name and its year in earth days.

    #. In ``templates/index``, create a table element and add the appropriate bootstrap class.
    #. The table can be styled to your liking. 
    #. Add a message to let the users know what data you are displaying with the ``yearLength`` field.

    .. sourcecode:: html
       :linenos:

       <table th:each="planet : ${planets}" class="table table-striped">
          <thead >
             <tr>
                <th th:text="${planet.name}">
                </th>
             </tr>
          </thead>
          <tr>
             <td th:text="${planet.yearLength} + ' Earth days in one year.'"></td>
          </tr>
       </table>

    :ref:`Back to the exercises <enums-exercises>`
