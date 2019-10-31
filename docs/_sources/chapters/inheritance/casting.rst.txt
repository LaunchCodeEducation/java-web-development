Casting
=======

.. index:: ! casting, ! polymorphism, ! runtime exception

When one class extends another, as ``HouseCat`` extends ``Cat``, a field
or local variable of the type of the base class may hold an object
that is of the type of the child class.

In other words, this is allowed:

.. sourcecode:: java

   Cat suki = new HouseCat("Suki", 8);

This is acceptable because a ``HouseCat`` *is a* ``Cat``. Furthermore,
when we call methods on such an object, the compiler is smart enough to
determine which method it should call. For example, the following call
to ``noise()`` will call the version defined in ``HouseCat``:

.. sourcecode:: java

   // Calls HouseCat's noise() method
   suki.noise(); // Hello, my name is Suki!

This only works for methods that are declared in the base class,
however. If we have a ``HouseCat`` object stored in a ``Cat`` variable
or field, then it is *not* allowed to call methods that are only part
``HouseCat``.

.. sourcecode:: java

   // Results in a compiler error, since Cat
   // doesn't have such a method
   suki.isSatisfied();

Here, ``isSatistfied()`` is defined in ``HouseCat``, and there is not a
corresponding overridden method in ``Cat``. If we were *really, really*
sure that we had a ``Cat`` that was actually a ``HouseCat``, we could
call such a method by first casting:

.. sourcecode:: java

   // As long as suki really is a HouseCat, this works
   ((HouseCat) suki).isSatisfied();

The danger here is that if ``suki`` is in fact not a ``HouseCat`` (it
was declared only as a ``Cat``, after all) then we’ll experience a
runtime exception. A **runtime exception** is an error that occurs upon
running the program, and is not found by the compiler beforehand. These
are dangerous, and situations where they might come up should be
avoided. So you should only cast an object to another type when you are
very sure that it’s safe to do so.

Storing objects of one type (e.g. ``HouseCat``) in a variable or field
of another “compatible” type (e.g. ``Cat``) is an example of
**polymorphism**. Polymorphism is another one of the pillars of OOP and we’ll 
have more to say about it in a future lesson.

References
----------

-  `Polymorphism
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html>`__

