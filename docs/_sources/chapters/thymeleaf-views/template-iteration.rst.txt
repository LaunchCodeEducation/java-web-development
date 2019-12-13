.. _thymeleaf-iteration:

Iterating in a Template
========================

Let's revisit part of the non-efficient HTML from the introduction, where we
hard-coded coffee options in a list.

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

.. sourcecode:: java

   for (Type item : collectionName) {
      // Code to repeat...
   }

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
#. The ``${}`` specifies the data provided by the controller.

We can think of a ``th:each`` statement as saying, *"For each item within
'collectionName', repeat this HTML tag, but use the current value of
'variableName'."*

Let's apply ``th:each`` to the HTML example above. Assume that we store each of
the coffee names as a string in an ArrayList called ``coffeeOptions``.

.. sourcecode:: html
   :linenos:

   <ol>
      <li th:each="item : ${coffeeOptions}" th:text="${item}"></li>
   </ol>

Some points to note:

#. ``coffeeOptions`` is passed into the template by the controller.
#. In the first pass through the loop, ``item`` takes the value of the first
   coffee name in the ArrayList.
#. ``th:text="${item}"`` displays the value of ``item`` in the view, so the
   ``li`` element will show the first coffee name.
#. Each successive iteration, ``item`` takes the next value in the list, and
   Thymeleaf adds a new ``<li></li>`` element to display that data.

.. _location-matters:

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

.. _th-block:

``th:block``
-------------

``th:block`` is a Thymeleaf *element* rather than an attribute, and it has the
general syntax:

.. sourcecode:: html
   :linenos:

   <th:block>
      <!-- Your HTML code -->
   </th:block>

``th:block`` allows you to apply the same Thymeleaf attribute, like ``th:if``
or ``th:each`` to a block of code. For example, assume you have an ArrayList
of coffee objects, each of which contains a ``name`` and ``description`` field.
If you want to display this information as name/description pairs, you might
try:

.. sourcecode:: html
   :linenos:

   <h3 th:each = "coffee : ${coffeeOptions}" th:text = "${coffee.name}">Coffee Name</h3>
   <p th:each = "coffee : ${coffeeOptions}" th:text = "${coffee.description}">Info</p>

However, ``th:each`` operates on and repeats a single HTML element. Instead of
alternating name/description pairs, the view in this case displays ``h3``
headings for all of the coffee names *before* rendering the ``p`` elements for
the descriptions.

To replicate the ``h3`` and ``p`` elements as pairs, you need to wrap them
inside ``th:block``:

.. sourcecode:: html
   :linenos:

   <th:block th:each = "coffee : ${coffeeOptions}">
      <h3 th:text = "${coffee.name}">Coffee Name</h3>
      <p th:text = "${coffee.description}">Info</p>
   </th:block>

Set up this way, the code gets interpreted as, *"Repeat the following HTML
elements once for each item in 'coffeeOptions'."* Each iteration of
the loop renders a heading/paragraph pair using a new ``coffee`` object from
``coffeeOptions``.

.. admonition:: Note

   Unlike a standard HTML tag (like ``div``, ``ul``, ``p``, etc.), the
   ``th:block`` element does NOT get rendered in the view.

.. admonition:: Tip

   To see an example for how to use ``th:block`` and iteration to produce a
   table, check the `Thymeleaf docs <https://www.thymeleaf.org/doc/tutorials/2.1/usingthymeleaf.html#synthetic-thblock-tag>`__.

Readability and Nested Loops
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``th:block`` helps clarify your HTML code by placing related Thymeleaf
attributes into separate tags.

.. admonition:: Examples

   This code generates multiple ``li`` elements and text by putting two
   attributes inside of the tag:

   .. sourcecode:: html
      :linenos:

      <ol>
         <li th:each="item : ${coffeeOptions}" th:text="${item}"></li>
      </ol>

   The code below accomplishes the same thing, but it separates the loop command
   from the ``th:text`` command:

   .. sourcecode:: html
      :linenos:

      <ol>
         <th:block th:each="item : ${coffeeOptions}">
            <li th:text="${item}"></li>
         </th:block>
      </ol>

   The second format more closely mimics the appearance of a Java ``for/each``
   loop, which improves the clarity of your code.

   .. sourcecode:: java
      :linenos:

      for (Coffee item : coffeeOptions) {
         // Code using the "item" variable...
      }

``th:block`` also allows you to set up nested loops:

.. admonition:: Example

   Assume you have a collection of different coffee shop objects, and each
   object stores a ``name`` and a list of ``coffeeOptions``. To display a list
   of lists:

   .. sourcecode:: html
      :linenos:

      <th:block th:each = "shop : ${shops}">  <!-- Iterate through shops -->
         <p th:text = "${shop.name}">Shop name</p>
         <ul>
            <!-- Iterate through coffeeOptions -->
            <th:block th:each = "flavor : shop.coffeeOptions">
               <li th:text="${flavor}"></li>
            </th:block>
         </ul>
      </th:block>

Check Your Understanding
-------------------------

Use the three code samples listed in the
:ref:`Location Matters <location-matters>` section to answer the following
questions:

.. admonition:: Question

   Which option produces one heading, 4 ordered lists, and 4 coffee names (each
   name labeled as "1")?

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
