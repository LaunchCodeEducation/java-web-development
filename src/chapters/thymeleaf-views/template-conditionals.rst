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
#. Alternatively, ``condition`` could also be a comparison that evaluates to
   ``true`` or ``false``.

.. admonition:: Note

   ``condition`` could also represent a function call that returns a boolean.
   However, making this work properly is an advanced topic and is beyond the
   scope of this course.

If ``condition`` evaluates to ``true``, then the HTML element gets added to
the webpage, and the content gets displayed. If ``condition`` is ``false``,
then the element is NOT generated, and the content stays off the page.

.. admonition:: Example

   Assume that ``coffeeOptions`` and ``userSelection`` represent an ArrayList
   and String, respectively, that are passed in by the controller.

   .. sourcecode:: html
      :linenos:

         <ol th:if = "${coffeeOptions.size() > 0}">
            <li th:each="item : ${coffeeOptions}" th:text="${item}"></li>
         </ol>

         <h2 th:if = '${userSelection.equals("instant")}'>You can do better!</h2>

*More words here...*

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
when the condition evaluates to ``false``. Thymeleaf provides a similar option,
but 

Try It!
--------

Video goes here...

Check Your Understanding
-------------------------

Questions go here...
