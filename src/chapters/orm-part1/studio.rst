.. _orm1-studio:

Studio: Creating an ``AbstractEntity``
======================================

In :ref:`orm1-exercises`, you created a new persistent class, ``EventCategory``. We will eventually use this class to categorize events in our application. However, your application now has a fair amount of duplication across the two model classes. In this studio, you will reduce repetition (i.e. "DRY out your code") using inheritance and abstract classes.

Getting Ready
-------------

In your ``coding-events`` repository, checkout out the ``add-persistent-category`` branch and create a new branch, ``abstract-entity-studio``, off of that branch.

.. admonition:: Note

   You can also branch off of the branch you created in the exercises, if you like. We have provided the branch mentioned to make sure you have good starter code for the studio, even if you didn't complete the exercises. 

Your Tasks
----------

Let's look at both the ``Event`` and ``EventCategory`` classes. There are four class members that are (essentially) the same in both classes:

- The ``id`` field
- The ``getId`` method
- The ``equals`` method
- The ``hashCode`` method

.. admonition:: Note

   If you have a super-sharp eye, you'll notice that the two ``equals`` methods aren't *exactly* the same. For example, the next-to-last line of this method in ``Event`` looks like this:

   .. sourcecode:: java

      Event event = (Event) o;

   while in ``EventCategory`` this line is slightly different;

   .. sourcecode:: java

      EventCategory that = (EventCategory) o;

   This minor difference will not matter in the long run, as we'll see later.

Your objective in this studio is to reduce this repetition by creating a class that contains the duplicated/shared code, which both ``Event`` and ``EventCategory`` can inherit.

Create and Extend ``AbstractEntity``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the ``models`` package, create a new class named ``AbstractEntity``. Add the ``abstract`` keyword to the class declaration. We do this because, while we want to share code across our two models, we'll never need to create an instance of ``AbstractEntity``. If you need a quick refresher, review our section on :ref:`abstract-classes`.

.. admonition:: Tip

   This class name seems a little odd at first, but it makes sense after a brief explanation. 
   
   It is a commonly used convention in Java to prefix the name of an abstract class with ``Abstract``, to make it obvious to other developers that they can't create instances of the class. 

   Additionally, *every* entity class that we create will extend ``AbstractEntity``. (Recall that an entity is a class/object that can be stored in a database.)

Finally, in the class declarations of both ``Event`` and ``EventCategory``, extend ``AbstractEntity``.

Move Duplicated Code Into the Superclass
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open up the ``Event`` class file. Move the 4 class members that we identified as being duplicated across both models up into ``AbstractEntity``. Now your ``Event`` class will *inherit* these members rather than define them itself.

When you move the ``equals`` method up into ``AbstractEntity``, you'll see a compiler error on the last line (this is related to the note we made above). Let's look at this method in detail.

.. sourcecode:: java
   :lineno-start: 22

   @Override
   public boolean equals(Object o) {
      if (this == o) return true;
      if (o == null || getClass() != o.getClass()) return false;
      Event event = (Event) o;
      return id == event.id;
   }

The compiler error occurs on the last line, and the context menu in IntelliJ describes it for us:

::

   'id' has private access in 'org.launchcode.codingevents.models.AbstractEntity'


What is this telling us? As written, ``event`` is an ``Event`` object, since it is the result of casting ``o`` to ``Event`` in the line above: ``Event event = (Event) o;``. But when we reference ``event.id`` we are attempting to reference the *private* field ``id``, which lives not in ``Event`` but in ``AbstractEntity``. This is not allowed.

This error is easy to fix; simply change the cast on the next-to-last line to convert ``o`` to an instance of ``AbstractEntity``. And while we're at it, let's give the variable ``event`` a better name.

.. sourcecode:: java
   :lineno-start: 22

   @Override
   public boolean equals(Object o) {
      if (this == o) return true;
      if (o == null || getClass() != o.getClass()) return false;
      AbstractEntity entity = (AbstractEntity) o;
      return id == entity.id;
   }

.. admonition:: Note

   The ``equals`` method works by checking the value of the identifier/primary key field ``id``. If two objects have the same ``id``, then they should be considered equal. Otherwise, they are not equal.

   It may not be obvious that you can't have an ``Event`` object and an ``EventCategory`` object with the same ``id``. However, the way in which the database manages and assigns these values ensures that won't happen.

Now in your the ``EventCategory`` model, delete the four class members that are now inherited from ``AbstractEntity``. You should have NO compiler errors in your application at this point.

The ``@MappedSuperclass`` Annotation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

One final step: Add the ``@MappedSuperclass`` to your ``AbstractEntity`` class. 

This annotation will be discussed in more detail later. For now, you should understand that it ensures that the ``id`` values will still be stored in the ``event`` and ``event_category`` tables of the database, even though ``Event`` and ``EventCategory`` don't have ``id`` fields in their class definition.

Making Sure It Works
--------------------

Start up your application and make sure it all works! Be sure to add some new data and make sure you see it in the appropriate table(s).
