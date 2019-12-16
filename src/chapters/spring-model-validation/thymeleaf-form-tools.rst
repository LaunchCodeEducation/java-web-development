Thymeleaf Form Tools
====================

Thymeleaf provides some handy attributes for working with form fields. They make use of the fact that, when using model binding, each model field contains a lot of information about the corresponding form input needed. In particular, the model field and its annotations often determine:

#. The name of the form field (that is, the value of its ``name`` attribute).
#. The input type, based on the data type of the field.
#. The validation rules and corresponding error messages for the field.

For example, a ``String`` field such as ``description`` often uses an ``input`` of ``type=text``. Thymeleaf provides some convenient attributes to make wiring up a form much easier and cleaner.

Display Validation Errors for a Field - Video
----------------------------------------------

.. raw:: html

   <div style="text-align:center;"><iframe width="800" height="450" src="https://www.youtube.com/embed/yc-bSDSDuKg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

The final code from this video is in the `display-errors branch <https://github.com/LaunchCodeEducation/coding-events/tree/display-errors>`__ of ``coding-events``.

Display Validation Errors for a Field - Text
--------------------------------------------

Using ``th:field``
^^^^^^^^^^^^^^^^^^

Using ``th:errors``
^^^^^^^^^^^^^^^^^^^
