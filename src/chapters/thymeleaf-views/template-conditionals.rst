Conditionals in a Template
===========================

In addition to iteration, Thymeleaf can also add or remove content on a
webpage based on certain conditions. Going back to the coffee example, we could
generate the ordered list ONLY IF ``coffeeOptions`` contains data. If the
ArrayList is empty, then there is no need to include the ``<ol>`` element.
Instead, the template could include a ``<p>`` element with text stating that
there are no options to select.

Just like the ``for/each`` syntax differs between Java and Thymeleaf, we need
to examine how to include *conditionals* in our templates. The logic remains
the same, but the implementation requires practice.

Display Content ``if``
-----------------------

The general syntax for including a conditional in Thymeleaf is:

.. sourcecode:: groovy

   th:if = "${condition}"

#. The ``th:if`` statement gets placed inside an HTML tag.
#. ``condition`` represents a boolean variable provided by the controller.
#. Alternatively, ``condition`` can be a statement that evaluates to ``true``
   or ``false``.

.. admonition:: Note

   ``condition`` could also represent a function call that returns a boolean.
   However, making this work properly is an advanced topic and is beyond the
   scope of this course.

If ``condition`` evaluates to ``true``, then Thymeleaf adds the HTML element to
the webpage, and the content gets displayed in the view. If ``condition`` is
``false``, then Thymeleaf does NOT generate the element, and the content stays
off the page.

.. admonition:: Example

   Assume that ``coffeeOptions`` and ``userSelection`` represent an ArrayList
   and String, respectively, that are passed in by the controller.

   .. sourcecode:: html
      :linenos:

         <ol th:if = "${coffeeOptions.size() > 1}">
            <li th:each="item : ${coffeeOptions}" th:text="${item}"></li>
         </ol>

         <h2 th:if = '${userSelection.equals("instant")}'>You can do better!</h2>

The conditional in line 1 checks that ``coffeeOptions`` contains more than one
item. If ``true``, then the ordered list is rendered in the view. The
``th:if`` statement in line 5 compares a user's flavor choice to the string
``"instant"``. If they match, then Thymeleaf adds the heading element to the
view.

Adding vs. Displaying/Hiding
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``th:if`` determines if content is *added or not added* to a page. This is
different from deciding if content should be *displayed or hidden*.

*Hidden* content still occupies space on a page and requires some amount of
memory. When ``th:if`` evaluates to ``false``, content remains absent from the
page---requiring neither space on the page nor memory. This is an important
consideration when including items like images or videos on your website.

``unless`` Instead of ``else``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In Java, we use an ``if/else`` structure to have our code execute certain steps
when a variable or statement evaluates to ``true`` but a different set of steps
for a ``false`` result. Thymeleaf provides a similar option with ``th:unless``:

.. sourcecode:: groovy

   th:unless = "${condition}"

Just like ``th:if``, the ``th:unless`` attribute gets placed inside an HTML
tag. In this case, however, Thymeleaf adds the HTML element to the webpage when
``condition`` evaluates to ``false``.

We could update our coffee code with an ``unless``:

.. admonition:: Example

   .. sourcecode:: html
      :linenos:

         <ol th:if = "${coffeeOptions.size() > 1}">
            <li th:each="item : ${coffeeOptions}" th:text="${item}"></li>
         </ol>

         <h2 th:unless = '${userSelection.equals("instant")}'>Excellent choice!</h2>

As long as ``userSelection`` is NOT ``"instant"``, the condition in line 5
evaluates to ``false``, and the ``h2`` element gets added to the view.

If we want to set up a situation for *If true, do this. Otherwise, do this
other thing*, we need to pair a ``th:if`` with a ``th:unless``.

.. admonition:: Example

   .. sourcecode:: html
      :linenos:

         <ol th:if = "${coffeeOptions.size()}">
            <li th:each="item : ${coffeeOptions}" th:text="${item}"></li>
         </ol>

         <p th:unless = "${coffeeOptions.size()}" th:text="${coffeeOptions.get(0)}"></p>

*More words here...*

Logical Operators
^^^^^^^^^^^^^^^^^^

We can use logical operators with ``th:if`` and ``th:unless``. The Thymeleaf
syntax for these is as follows:

#. Logical AND = ``and``,

   .. sourcecode:: groovy

      th:if = "${condition1 and condition2 and...}"
      // Evaluates to true if ALL conditions are true

#. Logical OR = ``or``,

   .. sourcecode:: groovy

      th:if = "${condition1 or condition2 or...}"
      // Evaluates to true if ANY condition is true

#. NOT = ``!``, ``not``.

   .. sourcecode:: groovy

      th:if = "${!condition}"
      // Evaluates to true when condition is false

What is ``true``?
^^^^^^^^^^^^^^^^^^

The ``th:if = "${condition}"`` attribute can evaluate more than simple boolean
variables and statements. It will also return ``true`` according to these
rules:

#. If ``condition`` is a boolean or statement and ``true``.
#. If ``condition`` is a non-zero number or character.
#. If ``condition`` is a string that is NOT ``"false"``, ``"off"``, or
   ``"no"``.
#. If ``condition`` is a data type other than a boolean, number, character, or
   String.

``th:if`` will evaluate to ``false`` whenever ``condition`` is ``null``.

Try It!
--------

Video goes here...

Check Your Understanding
-------------------------

Questions go here...
