Validation Annotations
======================

Within the model of a Java web application, we can define validation rules using annotations from the ``javax.validation.constraints`` package. This package provides a variety of annotations that are useful in common circumstances, and which can be applied to model fields. 

Common Annotations
------------------

We'll use only a few of these annotations, but you can find a full list in the `package documentation <https://docs.jboss.org/hibernate/beanvalidation/spec/2.0/api/>`_.

.. list-table:: Common Validation Annotations
   :header-rows: 1

   * - Annotation
     - Description
     - Syntax
   * - ``@Size``
     - Specifies minimum and/or maximum length for a string.
     - ``@Size(min = 3, max = 12)``
   * - ``@Min``
     - Specifies the minimum value of a numeric field.
     - ``@Min(0)``
   * - ``@Max``
     - Specifies the maximum value of a numeric field.
     - ``@Max(365)``
   * - ``@Email``
     - Specifies that a string field should conform to email formatting standards.
     - ``@Email``
   * - ``@NotNull``
     - Specifies that a field may not be ``null``.
     - ``@NotNull``
   * - ``@NotBlank``
     - Specifies that a string field contains at least one non-whitespace character.
     - ``@NotBlank``

.. admonition:: Example

   To apply the validation rules of the :ref:`example on the previous page <validation-example>` to the fields of a ``User`` model class, we can use ``@Size`` and ``@NotBlank``.

   .. sourcecode:: java

      @NotBlank
      @Size(min = 3, max = 12)
      private String username;

      @NotBlank
      @Size(min = 6)
      private String password;

Defining Validation Messages
----------------------------

.. index::
   single: validation, message

Each of these annotations takes and optional ``message`` parameter that allows you to define a user-friendly description to be used when validation fails.

.. admonition:: Example

   .. sourcecode:: java

      @NotBlank
      @Size(min = 3, max = 12, message = "Username must be between 3 and 12 characters long")
      private String username;

      @NotBlank
      @Size(min = 6, message = "Sorry, but the given password is too short. Passwords must be at least 6 characters long.")
      private String password;

We will see how to ensure these messages are properly displayed in the next section, :ref:`validating-models`.

Applying Validation Annotations - Video
---------------------------------------

.. raw:: html

   <div style="text-align:center;"><iframe width="800" height="450" src="https://www.youtube.com/embed/1aZxU0-dhgw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

The final code from this video is in the `add-validation-annotations branch <https://github.com/LaunchCodeEducation/coding-events/tree/add-validation-annotations>`__ of ``coding-events``.

Applying Validation Annotations - Text
--------------------------------------
