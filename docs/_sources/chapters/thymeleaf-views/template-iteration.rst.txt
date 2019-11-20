Iterating in a Template
========================

Let's revisit part of the non-efficient HTML from the introduction, where we
hard-coded the items in a list.

.. sourcecode:: html
   :linenos:

   <ol>
      <li>French Roast</li>
      <li>Espresso</li>
      <li>Kopi Luwak</li>
      <li>Instant</li>
   </ol>

If we want to add, remove, or edit the list items, we need to go in and change
the individual tags, which is a poor use of our time. Fortunately, there is a
way to streamline the process.

In Java, we use ``for/each`` loops to iterate through the items in a data
collection.

.. sourcecode:: Java

   for (Type item : collectionName)

Thymeleaf gives us a similar functionality to use in our templates, but we
need to learn a different syntax.

``th:each``
------------

The general syntax for iterating through a collection in Thymeleaf is:

.. sourcecode:: groovy

   th:each = "variableName : ${collectionName}"

#. The ``th:each`` statement gets placed INSIDE an HTML tag.
#. ``collectionName`` represents an ArrayList, HashMap, or other collection.
#. ``variableName`` represents an individual item or element within the
   collection.
#. The ``${}`` specifies the data that will be provided by the controller.

We can think of a ``th:each`` statement as, *For each item within
collectionName, repeat this HTML tag, but use the current value of
variableName*.

Let's apply ``th:each`` to the HTML list example above. We can assume that we
store each of the coffee names (French Roast, etc.) as strings in a ArrayList
called ``coffeeOptions``.

.. sourcecode:: html
   :linenos:

   <ol>
      <li th:each="item : ${coffeeOptions}" th:text="${item}"></li>
   </ol>

Some points to note:

#. ``coffeeOptions`` is passed into the template by the controller.
#. In the first pass through the loop, ``item`` takes the value of the first
   coffee name in the ArrayList.
#. ``th:text=${item}`` displays the value of ``item`` in the view, so the
   ``li`` element will show the first coffee name.
#. Each successive iteration, ``item`` takes the next value in the list, and
   Thymeleaf adds a new ``<li>`` tag to display that data.

Location Matters
^^^^^^^^^^^^^^^^^

``th:each`` creates one HTML tag for each item in a collection, and only one
``th:each`` statement can be placed in a given tag. BE CAREFUL where you place
it.

Consider the following code blocks:

.. admonition:: Examples

   Option #1:

   .. sourcecode:: html
      :linenos:

      <div>
         <h3>Java Types</h3>
         <ol>
            <li th:each="item : ${coffeeOptions}" th:text="${item}"></li>
         </ol>
      </div>

   Option #2:

   .. sourcecode:: html
      :linenos:

      <div>
         <h3>Java Types</h3>
         <ol th:each="item : ${coffeeOptions}">
            <li th:text="${item}"></li>
         </ol>
      </div>

   Option #3:

   .. sourcecode:: html
      :linenos:

      <div th:each="item : ${coffeeOptions}">
         <h3>Java Types</h3>
         <ol>
            <li th:text="${item}"></li>
         </ol>
      </div>

Which option produces:

#. One heading, 4 ordered lists, and 4 coffee names (each name labeled as "1")?
#. One heading, one ordered list, and 4 coffee names (with the names labeled
   1, 2, 3...)?
#. 4 headings, 4 ordered lists, and 4 coffee names (each name labeled as "1")?

``th:block``
-------------

Lorem ipsum...

Try It
-------

Video goes here?

Check Your Understanding
-------------------------

.. admonition:: Question

   Given the HTML examples above, which one produces one heading, 4 ordered
   lists, and 4 coffee names (each name labeled as "1")?

   #. Option 1
   #. Option 2
   #. Option 3

.. Answer = option 2

.. admonition:: Question

   Which option produces one heading, one ordered list, and 4 coffee names
   (with the names labeled 1, 2, 3...)?

   #. Option 1
   #. Option 2
   #. Option 3

.. Answer = option 1

.. admonition:: Question

   Which option produces 4 headings, 4 ordered lists, and 4 coffee names
   (each name labeled as "1")?

   #. Option 1
   #. Option 2
   #. Option 3

.. Answer = option 3
