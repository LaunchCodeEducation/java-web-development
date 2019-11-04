Studio: Sorting Cities
=======================

This studio has some starter code. So let's get it set up first. You might
enjoy `some music <https://www.youtube.com/watch?v=jJMxwBmQWHA>`__ while you do
so.

Getting Ready
--------------

Set up a local copy of the project:

#. Visit the `repository page <https://github.com/LaunchCodeEducation/sorting-cities>`__
   for this project and fork the repository to create a copy under your own
   GitHub account.
#. Back in IntelliJ, if you have a project open, select *File > Close Project*.
#. On the IntelliJ welcome screen, click *Check out from Version Control*,
   select Github.
#. Choose your fork from the repository dropdown, select the parent directory
   where you'd like to store your project, and hit *Clone*.
#. In the first modal screen, select *Create project from existing sources*.
   Accept the default settings on all other screens.

Cities Project Overview
------------------------

The project contains a data file, ``city_data.csv``, that contains data on over
300 U.S. cities. It has columns representing name, state, population (from the
2010 census) and land area (in square miles).

There is also a ``City`` class. This class encapsulates the same properties
contained in our data file, along with a couple of methods to make printing
information about cities easier.

The class ``CityData`` has a static ``loadData`` method that opens the CSV
file and parses it, returning a list of ``City`` objects.

Within ``Main.java``, we load the data, sort the list of ``City`` objects by
the ``name`` property, and print it out. Here's part of that code:

.. sourcecode:: java
   :lineno-start: 11

   ArrayList<City> cities = CityData.loadData();  // Loads the CSV data into the 'cities' list


   NameComparator comparator = new NameComparator();
   cities.sort(comparator);  // Sorts the 'cities' list alphabetically

   printCities(cities); // Prints the items from the 'cities' list

Go ahead and run the ``main`` method to see how the program displays the city
data.

Sorting Cities
~~~~~~~~~~~~~~~

To sort the ``cities`` list, we use the ``NameComparator`` class, which is
located in the ``org.launchcode.comparators`` package of the project.

``NameComparator`` implements ``Comparator<City>`` which provides the
``compare(City, City)`` method.

#. ``compare(City, City)`` takes two ``City`` objects and determines which one
   should be ordered before the other.
#. Sorting by name is just ordering the ``City`` objects alphabetically by
   their ``name`` fields. Thus, ``NameComparator`` uses the ``compareTo``
   method of the ``String`` class and passes in the ``name`` properties of the
   two input objects. This occurs in line 14 of the class:

   .. sourcecode:: java
      :lineno-start: 10

      public class NameComparator implements Comparator<City> {

         @Override
         public int compare(City o1, City o2) {
            return o1.getName().compareTo(o2.getName());
         }
      }

#. ``compareTo`` is the *instance version* of ``Comparator.compare``. It
   returns integers based on the two inputs, and it can be called on a
   ``String`` instance rather than on a ``Comparator`` instance.
#. The ``Comparator<T>`` interface contains the method ``compare(T, T)``. This
   method returns an integer that determines which of the two objects comes
   before the other, or is *less than* the other. If the returned integer is
   less than zero, then the first parameter comes before the second. If the
   value is zero, then the parameters are the same in terms of ordering. If the
   value is greater than zero, then the second parameter comes before the
   first.

.. admonition:: Tip

   Think of the result returned by calling ``compare(x, y)`` as being the
   *value* of calculating ``x - y``. If ``x`` is smaller than ``y``, the value
   is negative, and ``x`` should be ordered first. If ``x`` is larger than
   ``y``, the result is positive, and ``y`` comes first.

To sort the list, the comparator object is passed in to the ``sort`` method for
it to use. The list is sorted *in place*. Rather than returning a new list that
is sorted, ``sort`` modifies the given list by reordering its contents.

Your Task
----------

Using ``NameComparator`` and the `Comparator documentation <http://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html>`__
as guidance, implement AT LEAST TWO of the following comparators:

#. ``StateComparator`` - Produces an alphabetical sorting by state.
#. ``PopulationComparator`` - Results in a sorting by population, from
   *largest* to *smallest* size.
#. ``AreaComparator`` - Results in a sorting by land area, from *largest* to
   *smallest* size.

Place your new comparators in the `org.launchcode.comparators` package,
and they should implement ``Comparator<City>``.

Test each one by modifying the code in ``Main.java`` to assign the different
comparators.

Bonus Missions
---------------

Sort Based on Multiple Properties
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a ``CompoundComparator`` class that is able to order the cities based on
multiple factors. For example, we should be able to order alphabetically by
state name and then by population size.

Here are the steps to carry this out:

#. Create a class that implements ``Comparator<City>``.
#. Create a field ``comparators`` of type ``List<Comparator<City>>``.
#. Initialize ``comparators`` to be an empty list: ``new ArrayList<>()``. You
   can do this in a constructor, or in the same line that you declare the
   field.
#. Provide a method ``add(Comparator<City> newComparator)`` that adds a
   selected comparator to the ``comparators`` list.
#. You'll need the following method in order to implement the interface:

   .. sourcecode:: java

      @Override
      public int compare(City o1, City o2){
         // Your code here...
      }

   a. The method should apply each object in ``comparators`` in order. You'll
      first use ``comparators.get(0).compare(o1, o2)`` to sort ``o1`` and
      ``o2`` by the first comparator, then ``comparators.get(1)``, etc.
   b. You only need to move on to the next comparator in the list if the
      previous one returns ``0``.
   c. For example, assume you want to compare cities by state and then by
      population. When ordering St. Louis and Las Vegas, you do NOT need to
      compare population. St. Louis comes before Las Vegas because "Missouri"
      comes before "Nevada". However, when comparing St. Louis and Kansas City,
      you *would* need to compare population, since the cities are in the same
      state.

   .. admonition:: Tip

      We suggest using a ``while`` loop to do this, along with some variables to
      keep track of the list index and the ``compare`` result.

#. To use ``CompoundComparator``, create an instance of the class and then add
   individual comparators in the order that you want them to be used:

   .. sourcecode:: java
      :linenos:

      CompoundComparator comparator = new CompoundComparator();
      comparator.add(new StateComparator());
      comparator.add(new PopulationComparator());

Select the Sorting Method
~~~~~~~~~~~~~~~~~~~~~~~~~~

Prompt the user to decide how to sort the city data, and then implement the
chosen options.
