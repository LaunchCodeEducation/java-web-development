Exercises: Enum Practice
========================

#. Fork and clone `enumerable-planets <https://github.com/LaunchCodeEducation/enumerable-planets>`__.

#. Use the *Get from Version Control* option to open the project in IntelliJ.

#. In the project, navigate to the data package.

#. Create a new public enum called ``Planets``.

   .. sourcecode:: java

      public enum Planets {
         // list the planets here.
         // Mercury, Venus, Earth, Mars, Jupiter,
         // Saturn, Uranus, Neptune
         // Don't forget to capitalization convention and enum 
         // syntax to separate value and end the list
      }

#. Before adding any other fields to ``Planets``, go to ``PlanetController``
   and update the index handler to pass in a ``Model`` class argument (eg. ``Model model``). 

#. Use ``.addAttribute`` to add the planet values to the model.

#. In ``templates/index``, create a list element and use the template
   variable you have just defined in the controller to list all of the 
   planet values on the page.

#. Add a ``name`` field to the planets.

   a. Create a name property to display a non-capitalized version of each of the planet names.
   #. Add a constructor for with the name field and a getter for the field.

#. Update the template to display the planet names.

#. Back in the ``Planets`` enum, add a new field called ``yearLength``.

   #. The value of each ``yearLength`` should be the number of earth days of a year on the given planet.

      #. Number of earth days on each planet:

         #. Mercury: 88
         #. Venus: 225
         #. Earth: 365
         #. Mars: 687
         #. Jupiter: 4333
         #. Saturn: 10759
         #. Uranus: 30687
         #. Neptune: 60200

   #. Update the constructor and add a getter for this field.

#. Change the index template to display a table of each planet name and its year in earth days.

   #. In ``templates/index``, create a table element and add the appropriate bootstrap class.
   #. The table can be style to your liking and add a message to let the users know what data you are displaying
      with the ``yearLength`` field.

#. If you wish, add another field to ``Planets``. You can find plenty of information on `NASA's web site <https://solarsystem.nasa.gov/planets/overview/>`__.

   #. Update the enum with the new field, including changing the constructor and adding a getter method.
   #. Add the field to display in the table, with a message if helpful to convey the information or units of measure.
   