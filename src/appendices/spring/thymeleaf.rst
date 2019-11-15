.. _thymeleaf-commands:

Thymeleaf Commands
==================

Thymeleaf is a template engine and Thymeleaf templates make up the views of our MVC application.
In order to create our templates, we use attributes to pass data through controllers to our views out of the model.

Attributes
----------

Thymeleaf has many attributes that we could use. In this book, we focus on a few key ones.

Displaying Data
^^^^^^^^^^^^^^^

``th:text`` dynamically populates the contents of an HTML element.

.. sourcecode:: html

   <p th:text = "Hello from Thymeleaf!">text</p>

If we want to pull in a value of a variable from the controller, we can use the **variable expressions** syntax, ``${}``.

.. sourcecode:: html

   <p th:text = "${message}">text</p>

Conditionally Displaying Data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``th:if`` will display the value if the expression evaluates to true.
``th:unless`` will display the value if the expression evaluates to false.

Iteration
^^^^^^^^^

``th:each`` used in conjunction with the ``th:block`` to iterate through items in an ArrayList.
``th:block`` see above.

Template Fragments
^^^^^^^^^^^^^^^^^^

``th:fragment`` defines template fragments.
``th:replace`` defines template fragments.

Static Resources
^^^^^^^^^^^^^^^^

``th:src`` used to include static resources.
``th:href`` used to include static resources.

