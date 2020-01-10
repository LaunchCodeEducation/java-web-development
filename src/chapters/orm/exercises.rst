Exercises
=========

For the exercises, we are going to continue building on our ``coding-events`` application.

The ``EventCategory`` Class
---------------------------

We need to use the ``@Entity`` annotation to create a new class called ``EventCategory``.

Our class needs to have the following:

#. An ``id`` field.
#. A ``name`` field.
#. A constructor.
#. The appropriate getters and setters.

The ``EventCategoryRepository``
-------------------------------

Create the ``EventCategoryRepository`` in the ``data`` folder.

The ``EventCategoryController``
-------------------------------

Create the ``EventCategoryController`` in the ``controllers`` directory.

We will be creating 3 handlers in our controller:

#. ``displayAllEvents``
#. ``renderCreateEventCategoryForm``
#. ``processCreateEventCategoryForm``

Thymeleaf Templates
-------------------

To finish the exercises, we need to make two new templates.

#. ``eventCategories/index``
#. ``eventCategories/create``