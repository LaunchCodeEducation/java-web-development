Exercises: Interfaces and Polymorphism
=======================================

We've learned that ``ArrayList<T>`` implements both ``List<E>`` and
``Iterable<T>``. In fact, ``List<E>`` extends ``Iterable<T>``, which means that
``List<E>`` includes all of the contracted methods that ``Iterable<T>`` does.

Check out the documentation for `List<E> <https://docs.oracle.com/javase/8/docs/api/java/util/List.html>`__
and `Iterable<T> <https://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html>`__ to confirm for yourself!

   TODO: Revise instructions to reference new assignments/studios and remove
   Spring Boot requirements.

.. TODO: Revise instructions to reference new assignments/studios and remove
   Spring Boot requirements.

Open up your ``techjobs-mvc`` solution. Within ``ListController`` and
``SearchController``, change every local variable that's declared to be of
type ``ArrayList`` to be either a ``List`` or an ``Iterable``, using the least
restrictive type as possible. In other words, if you only need to loop over the
collection, use ``Iterable``, but if you also need to access elements of the
collection by index---as in, ``Type item = items.get(0)``---then use ``List``.
Be sure to look at the templates to see how collections being passed into the
templates are used. Also be sure to test your code after making these changes!
