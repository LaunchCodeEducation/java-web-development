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

   ArrayList<City> cities = CityData.loadData();


   NameComparator comparator = new NameComparator();
   cities.sort(comparator);

To sort the ``cities`` list, we use ``NameComparator``, which is located in the
``org.launchcode.comparators`` package of the project. ``NameComparator``
implements ``Comparator<City>`` by providing the ``compare(City, City)``
method, which compares two cities to determine which should be ordered before
the other. Since sorting by name is just sorting alphabetically by the ``name``
file, ``NameComparator`` uses the ``compareTo`` method of the ``String`` class
with the ``name`` properties of the given input parameters. ``compareTo`` is
the *instance version* of ``Comparator.compare``; it returns integers under the
same conditions, but can be called on a ``String`` instance rather than on a
``Comparator`` instance.

The ``Comparator<T>`` interface contains the method ``compare(T, T)``. This
method returns an integer that determines which of the two objects comes
before the other, or is *less than* the other. If the returned integer is less
than zero, then the first parameter comes before the second. If the value is
zero, then the parameters are the same in terms of ordering. If the value is
greater than zero, then the second parameter comes before the first.

.. admonition:: Tip

   Think of the result returned by calling ``compare(x, y)`` as being the
   *value* of calculating ``x - y``. If ``x`` is smaller than ``y``, the value
   is negative. If ``x`` is larger than ``y``, the result is positive.

In order to sort the list, the comparator object is passed in to the ``sort``
method for it to use. The list is sorted *in place*. Rather than returning a
new list that is sorted, ``sort`` modifies the given list by reordering its
contents.

Your Task
----------

Your task is to implement AT LEAST TWO of the following comparators:

#. ``StateComparator`` - Results in an alphabetical sorting by state.
#. ``PopulationComparator`` - Results in a sorting by population, from largest
   to smallest.
#. ``AreaComparator`` - Results in sorting by land area, from largest to
   smallest.

Your comparators should be placed in the `org.launchcode.comparators` package,
and they should implement ``Comparator<City>``. Test them out by modifying the
code in ``Main.java``.

Refer to ``NameComparator`` and the `Comparator documentation <http://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html>`__ for guidance.

Bonus Mission
--------------

Create a ``CompoundComparator`` class that is able to order the cities based on
multiple factors. For example, we should be able to order alphabetically by
state name and then by population size.

Here are the steps to carry this out:

#. Create a class that implements ``Comparator<City>``.
#. Create a field ``comparators`` of type ``List<Comparator<City>>``.
#. Initialize ``comparators`` to be an empty list: ``new ArrayList<>()``. You
   can do this in a constructor, or in the same line that you declare the
   field.
#. Provide a method ``add(Comparator<City>)`` that adds a comparator to the
   ``comparators`` list.
#. You'll need the following method in order to implement the interface:

   .. sourcecode:: java

      @Override
      public int compare(City o1, City o2)

   This method should use each object in ``comparators``, in order. You'll first
   use ``comparator.get(0)`` to compare ``o1`` and ``o2``.

   You only need to move on to the next comparator if the first comparator
   returns 0. For example, if you're comparing cities by state and then by
   population, when comparing St. Louis and New York, you don't need to compare
   population. You know that St. Louis comes before New York because
   "Missouri" comes before "New York". However, when comparing St. Louis and
   Kansas City, you would need to compare population, since the cities are in
   the same state.

   .. admonition:: Tip

      We suggest using a ``while`` loop to do this, along with some variables to
      keep track of the state.

#. To use ``CompoundComparator``, create an instance of the class and then add
   individual comparators in the order that want them to be used:

   .. sourcecode:: java
      :linenos:

      CompoundComparator comparator = new CompoundComparator();
      comparator.add(new StateComparator());
      comparator.add(new PopulationComparator());

