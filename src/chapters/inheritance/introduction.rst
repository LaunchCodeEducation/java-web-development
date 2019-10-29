A Tale of Two Cats
==================

.. index:: ! inheritance, ! subtyping

**Inheritance** is the second of the **Three Pillars of Object-Oriented
Programming** that we will encounter.

Here’s a definition: Inheritance is a mechanism within object-oriented programming that
allows one class to be based on another class, thus receiving its
properties and behaviors. 

.. note::

   Inheritance is also sometimes referred to as **subtyping**.


Inheritance in Java
-------------------

Let's examine an inheritance relationship between two classes, ``Cat`` and ``HouseCat``.
``HouseCat`` is a class that inherits from ``Cat``. When defined, ``HouseCat`` thus 
receives the data and behaviors of ``Cat``. These inherited traits are things like 
fields, properties, and methods. Any fields and non-constructor methods in ``Cat`` 
are be available to each instance of ``HouseCat``. 

.. index:: ! extends

When we speak about an inheritance relationship, we say that a ``HouseCat`` *is a* 
``Cat``, or *extends* ``Cat``. Indeed, in order to define a class that inherits from
another, we use the ``extends`` keyword.

.. sourcecode:: java
   :linenos:

   public class Cat {
       // ...code for the Cat class...
   }

   public class HouseCat extends Cat {
       // ...code for the HouseCat class...
   }

.. index:: ! subclass, ! derived class, ! child class, ! superclass, ! base class, ! parent class

We say that ``HouseCat`` is a **subclass**, **derived class**, or
**child class** of ``Cat``, and we say that ``Cat`` is the
**superclass**, **base class**, or **parent class** of ``HouseCat``. 

In Java, a class may extend only one class. Classes may extend each
other in turn, however. This creates hierarchies of classes. We often visualize these
by drawing each class as a box, with an arrow pointing from the subclass
to the base class.

.. figure:: figures/inheritance-basic.png
   :scale: 50%
   :alt: Basic inheritance diagram.

   ``B`` extends ``A``.

The shaded portion of these boxes can include additional information
about each class. We’ll learn about what we might put here in a future
lesson.

Inheritance is an essential mechanism for sharing data and behavior between
related classes. Using it effectively creates organized code with groups of classes
that have increasingly specialized behavior.

When this happens, we can visualize the inheritance structure with a
slightly more complex diagram.

.. figure:: figures/inheritance-tree.png
   :scale: 50%
   :alt: Multi-node inheritance tree.

   Inheritance tree with many nodes.

You can see that classes ``B``, ``C``, and ``D`` all extend class ``A``.
And class ``E`` extends class ``D`` which itself extends class ``A``. So
class ``E`` involves an even greater specialization of behavior than
class ``D``.

Fields and non-constructor methods are directly
available to instances of the subclass, subject to any access modifiers.
In general, this means that ``private`` and package-private
members of a base class are not accessible to a subclass. The exception
to this is that package-private members are accessible to subclasses
*within the same package*.

.. note::

   If anything in the last paragraph was fuzzy, this is a good time to review 
   :ref:`access modifiers in Java <access-modifiers>`.


Let’s revisit our ``Cat`` and ``HouseCat`` friends. In ``java-web-dev-exercises``,
open ``src/org/launchcode/java/demos/inheritance`` and examine the two classes inside.

Notice that ``Cat`` has a ``private`` string field ``family``, representing
the biological family of all cats. 

.. sourcecode:: java
   :lineno-start: 10

   private String family = "Felidae";

This field is not directly accessible by ``HouseCat`` since it is ``private``. 
However, it may be read via the public getter ``getFamily``. 

.. sourcecode:: java
   :lineno-start: 42

   public String getFamily() {
      return family;
   }

There is no setter for ``family``, however. It may only be set within ``Cat``. 
It makes sense that a subclass should not be able to change the biological family 
of a cat, since this field should rarely, if ever, change.

Methods of the base class ``Cat`` may be called on instances of the
subclass ``HouseCat`` as if they were defined as part of the
``HouseCat``.

Try it out. In your inheritance folder, create a ``Main`` class. Within that class,
write an instance of ``HouseCat`` and call some of the methods it inherits from ``Cat``.

.. sourcecode:: java
   :linenos:

   HouseCat garfield = new HouseCat("Garfield", 12);
   garfield.eat();
   System.out.println(garfield.isTired());   // prints true

The ``eat`` method was defined in ``Cat``, but may be called on all
``HouseCat`` instances as well. We say: “``HouseCat`` inherits the
method ``eat()`` from ``Cat``.” We know we have successfully called ``eat()`` on 
``garfield`` because the printed statement indicates the cat is now tired. 

``super``
---------

We mention above that a subclass inherits all *non-constructor*
methods from its base class. Indeed, when extending a class, we will not
be able to create new instances of our subclass ``HouseCat`` using any
constructors provided by ``Cat``. 

The base class ``Cat`` has a constructor that takes a single parameter
of type ``double``.

.. sourcecode:: java
   :lineno-start: 12

   public Cat (double aWeight) {
      weight = aWeight;
   }

But because ``HouseCat`` does not have such a constructor, the following code 
does not compile:

.. sourcecode:: java

   HouseCat mittens = new HouseCat(8.4);

.. index:: ! super,

``Cat`` constructors are not inherited by ``HouseCat``. If we want
to use a ``Cat`` constructor in this subclass, we must explicitly
provide it. 

To do so, look at the constructor included in ``HouseCat``:

.. sourcecode:: java
   :lineno-start: 7

   public HouseCat(String aName, double aWeight) {
      super(aWeight);
      name = aName;
   }

Here, the ``super`` keyword allows the subclass to access the constructor from the
base class. This call to the base class constructor must be the first line of 
the subclass constructor. In the case of ``HouseCat``, the subclass constructor 
extends the original constructor by setting an additional property, ``name``.

If a base class constructor takes no arguments, then the 
default constructor is implicitly called for you in the subclass. 

For example, we can add an additional constructor in ``Cat``:

.. sourcecode:: java
   :lineno-start: 16

   public Cat () {
      weight = 13;
   }

Then in ``HouseCat``, we can simply define another constructor as this:

.. sourcecode:: java
   :lineno-start: 12

   public HouseCat(String aName) {
      name = aName;
   }

Even though we don’t explicitly specify that we want to call a
constructor from ``Cat``, the default constructor will be called. Now, we can 
initialize a new ``HouseCat`` with only a ``name`` property and ``Cat`` default
constructor will still be applied. Back in ``Main``, you can confirm that the base
class constructor has been called:

.. sourcecode:: java
   :linenos:

   HouseCat spike = new HouseCat("Spike");
   System.out.println(spike.getWeight());   // prints 13

As a consequence of this constructor syntax, we can easily expose any
constructor from the base class by providing a subclass constructor with
the same signature and a body that only calls the base class
constructor.

.. sourcecode:: java
   :lineno-start: 16

   public HouseCat(double aWeight) {
      super(aWeight);
   }

.. warning::

   This constructor is a bad one, and is included merely to introduce
   syntax and usage. We would not want to have a constructor for
   ``HouseCat`` that didn’t initialize an essential field such as ``name``.

.. index:: ! @Override, ! method overriding

``@Override``
-------------

Sometimes when extending a class, we’ll want to modify behavior provided
by the base class. This can be done by replacing the implementation of
an inherited method by a completely new method implementation. For a
given method, we can do this via **method overriding**.

In our example, the ``noise`` method of ``HouseCat`` overrides the
method of the same name in ``Cat``. When we override it, we should use
the ``@Override`` annotation.

Here are the methods in question.

In ``Cat``:

.. sourcecode:: java
   :lineno-start: 69

   public String noise() {
      return "Meeeeeeooooowww!";
   }

In ``HouseCat``:

.. sourcecode:: java
   :lineno-start: 24

   @Override
   public String noise() {
      return "Hello, my name is " + name + "!";
   }

If we have a ``HouseCat`` object and call its ``noise()`` method, we will be 
using the method defined in ``HouseCat``.

.. sourcecode:: java
   :linenos:

   Cat plainCat = new Cat(8.6);
   HouseCat cheshireCat = new HouseCat("Cheshire", 12);

   System.out.println(plainCat.noise()); // prints "Meeeeeeooooowww!"
   System.out.println(garfield.noise()); // prints "Hello, my name is Cheshire!"


Similar to other :ref:`java-annotations`, the ``@Override`` annotation is 
not required. However, it can prevent unintentional errors, and makes it clear 
when reading your code what you intend to do. 

The compiler will see the annotation and check to ensure that the signatures 
of the base method and the overriding method match up. If they don’t, it will 
flag an error. This can help prevent you from inadvertently creating a method 
with a different signature.

.. warning::

   When overriding a method from a base class, the method signatures *must
   be exactly the same*. Recall that the signature of a method is the
   method name and access level, along with it’s return type and the type
   and number of input parameters.

   In this example, the signature of our method is:

   .. sourcecode:: java

      public String noise();

When overriding a method, we may call the method from the base class
that we are overriding by using ``super``. Modify your ``HouseCat.noise()``
method as follows:

.. sourcecode:: java
   :lineno-start: 29

   @Override
   public String noise() {
      if (isSatisfied()) {
         return "Hello, my name is " + name + "!";
      } else {
         return super.noise(); // prints "Meeeeeeooooowww!"
      }
   }

This calls the overridden method in the base class via
``super.noise()``, carrying out the original behavior if the given
conditional branch is reached.

.. index:: ! Object Class

``Object`` Class
----------------

In a previous lesson, we introduced the :ref:`special-methods` ``equals`` and
``toString``. All classes contain default implementations of these methods that 
can be overridden.

In fact, these default methods are part of a class called ``Object``. If
a class does not explicitly extend another class, then it implicitly
extends ``Object``. So the default implementations of ``equals`` and
``toString`` (along with a few `other
methods <https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#method.summary>`__)
are made available to us via inheritance.

Note that we should use the ``@Override`` annotation when we provide new
implementations of these methods as well.

.. index:: ! abstract classes

``abstract`` Classes
--------------------

We noted in the introduction to this section that inheritance is a way
to share behaviors among classes. You’ll sometimes find yourself
creating a base class as a way to share behaviors among related classes.
However, in such situations it is not always desirable for instances of
the base class to be created.

For example, suppose we began coding two classes, ``HouseCat`` and
``Tiger``. Upon writing the code, we realized that there was some common
data and behaviors. For example, they both make a noise, come from the
same biological family, and get hungry. In order to reduce code
repetition, we combined those in ``Cat`` (as above).

.. sourcecode:: java
   :linenos:

   public class Cat {
      // Cat class definition
   }

   public class HouseCat extends Cat {
      // HouseCat class definition
   }

   public class Tiger extends Cat {
      // Tiger class definition
   }

In reality, though, we might not want objects of type ``Cat`` to be
created, since such a cat couldn’t actually exist (a real cat would have
a specific genus and species, for example). We could prevent objects of
type ``Cat`` from being created, while still enabling sharing of
behavior among its subclasses, by making ``Cat`` an **abstract class**.

Change the signature on ``Cat``:

.. sourcecode:: java
   :linenos-start: 3

   public abstract class Cat
   {
      // Cat class definition
   }

Now, in ``Main``, if you try creating a new ``Cat`` object, 

.. sourcecode:: java

   Cat salem = new Cat(8);

IntelliJ has your back with a handy error message that an abstract class cannot be 
instantiated.

In order to use the behavior of an abstract class, *we
must extend it*.

.. index:: ! abstract methods

``abstract`` Methods
--------------------

We have another tool that we may use here, which is an **abstract
method**. An abstract method is a method in an abstract class that does
not have a body. In other words, it does not have any associated code,
only a signature. It must also be marked ``abstract``.

In our abstract ``Cat`` class, it would make sense to make an abstract
``noise`` method since all types of cats make noise. By creating this
abstract method, we force any class that extends ``Cat`` to provide its
own implementation of that behavior.

.. sourcecode:: java

   public abstract String noise();


Now, classes such as ``HouseCat`` and ``Tiger``, which both extend
``Cat``, *must* provide their own version of ``noise()``, with the exact
same method signature.

.. index:: ! casting, ! polymorphism, ! runtime exception

Casting
-------

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
**polymorphism**. We’ll have more to say about polymorphism in a future
lesson.

References
----------

-  `Inheritance in Java
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html>`__
-  `The @Override annotation
   (docs.oracle.com)] <https://docs.oracle.com/javase/8/docs/api/java/lang/Override.html>`__
-  `The Object Class
   (docs.oracle.com) <https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html>`__
-  `Abstract Classes and Methods
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/IandI/abstract.html>`__
-  `Polymorphism
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/IandI/polymorphism.html>`__

Check Your Understanding
------------------------

.. admonition:: Question

   For this question, refer to the code blocks below.

   .. sourcecode:: java

      public class Message {
         private boolean friendly = true;
         private String language;
         private String text;

         public Message(String aLanguage, String aText) {
            language = aLanguage;
            text = aText;
         }

         public boolean getFriendly() {
            return friendly;
         }

         public String getLanguage() {
            return language;
         }

         public String getText() {
            return text;
         }
      }

   A class called ``Greeting`` extends ``Message``. What would a constructor for 
   ``Greeting`` need to be to call the ``Message`` constructor?

   a. .. sourcecode:: java

         public Greeting(String aLanguage, String aText, boolean isFriendly) {
            super(aLanguage, aText);
            friendly = isFriendly;
         }
      
   b. .. sourcecode:: java

         public Greeting(String aLanguage, String aText) {
            super(aLanguage, aText);
         }

   c. .. sourcecode:: java

         public Greeting() {
            super(aLanguage, aText);
         }

   d. .. sourcecode:: java

         public Greeting(String aLanguage, String aText) {
            language = aLanguage;
            text = aText;
         }

.. ans: b, public Greeting(String aLanguage, String aText) {
            super(aLanguage, aText);
           }
           