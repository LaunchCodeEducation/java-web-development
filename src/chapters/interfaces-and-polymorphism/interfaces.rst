Interfaces
==========

Benefits of Using Interfaces
----------------------------

Interfaces are great! Trust us, they really are. Once you get used to
them, you’ll begin to think more abstractly about which *behaviors* your
code requires rather than which *classes* your code requires. This means
you’ll be able to “code to interfaces” (an OOP principle) instead of
coding to classes, and your code will become more flexible and
extensible.

Here are a few benefits of using interfaces:

-  You can only extend one class, but you may implement many interfaces.
-  You can extend a class and implement an interface at the same time.
-  By declaring variables and parameters as interface types, you make
   your code useful for a much wider variety of situations.
-  When you declare properties and return types to be interface types,
   you decouple code using your classes from the actual class types you
   use. This means that you are free to change the specific
   implementation of your classes without affecting those using them.
   For example, if from a public method you returned an object of type
   ``Iterable<Job>`` then you would be free to change the method’s
   internal structure to use, say, a
   `HashSet <http://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html>`__
   instead of an
   `ArrayList <http://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html>`__.

Remember that you don’t need to start creating interfaces to use their
power! When working with collections, in particular, think about the
behaviors that your code requires, and declare variables and parameters
to be interface types if you only need to use specific behaviors such as
ordering or iteration.

References
----------

-  `Interfaces
   Tutorial <https://docs.oracle.com/javase/tutorial/java/IandI/createinterface.html>`__
-  `Comparable
   Interface <http://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html>`__
-  `Comparator
   Interface <http://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html>`__
-  `Iterable
   Interface <http://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html>`__
-  `List
   Interface <http://docs.oracle.com/javase/8/docs/api/java/util/List.html>`__
-  `Map
   Interface <http://docs.oracle.com/javase/8/docs/api/java/util/Map.html>`__


An **interface** is a formal construction within Java that allows us to
create a contract that classes can choose to fulfill. A Java interface
may contain:

-  Constants (that is, ``static final`` fields)
-  Method signatures
-  Static methods
-  Default methods

.. raw:: html

   <aside class="aside-note">

An interface may also contain “nested types”, which we won’t discuss in
this class.

.. raw:: html

   </aside>

The most useful aspect of interfaces is to specify method signatures.
Recall that a method signature includes the name, parameters, and return
type of a method, but no body. From the list above, we’ve seen every
type of member except for **default methods**. We’ll describe these
briefly near the end of this lesson.

Here’s a simple example:

.. code:: java

   public interface Feedable
   {

       void eat();

   }

And here are some observations:

-  An interface is defined similarly to an abstract class, but using the
   keyword ``interface``. (We’ll discuss similarities and differences
   between interfaces and abstract classes below.)
-  ``eat`` only has a signature. We are not allowed to provide a body
   for methods defined in interfaces.
-  ``eat`` does not have an access modifier. Interface members are
   always ``public``, and while we may use the ``public`` modifier, it’s
   unnecessary. An interface method may not have an access modifier that
   is more restrictive than ``public``.
-  The interface itself is declared ``public``, which means any other
   class may use it. We may also leave off ``public``, making the
   interface package-private, or usable only within the same package.
-  The name is indicative of the behavior that the interface is intended
   to describe. While this is only a convention, most interfaces have
   names that are adjectives. Whatever you do, use meaningful names!

The purpose of an interface is to define a contract that classes may
choose to uphold. In doing so, we say that they “*implement* the
interface”. The syntax for implementation is similar to that for
inheritance. Here’s how we can use the ``Feedable`` interface in
defining our ``Cat`` class.

.. code:: java

   public class Cat implements Feedable
   {

       @Override
       public void eat()
       {
           // method implementation
       }

       // ...rest of the class definition...

   }

Since we’ve declared that ``Cat`` implements ``Feedable``, we have to
provide an implementation for the ``eat`` method, with the signature as
specified in the interface definition. Note that we use ``@Override``,
just as we do when overriding an inherited method in a subclass. Like
that situation, using ``@Override`` when implementing methods defined in
an interface will enable the compiler to check that your method
signature does indeed match that of the interface.

.. raw:: html

   <aside class="aside-note">

You may both extend a class and implement an interface at the same time:

.. code:: java

   public class MyClass extends MySubclass implements MyInterface
   {
       // ...code...
   }

.. raw:: html

   </aside>

As with classes, interfaces define a type that can be used when
declaring fields, parameters, and local variables.

Using an interface allows us to relax the requirements on our code
elsewhere, thus making it more extensible and adaptable. For example,
here’s how we might modify ``CatOwner``:

.. code:: java

   public class CatOwner
   {
       private Feedable pet;

       public CatOwner(Feedable pet) {
           this.pet = pet;
       }

       public  void feedTheCat() {

           // ...code to prepare the cat's meal...

           pet.eat();
       }
   }

Note that we’ve declared the property ``pet`` to be of type
``Feedable``. This class assumes that the only behavior of ``pet`` that
we’ll need within the class is the ability to ``eat``. But if that’s all
we need, then we should relax the requirements on the ``pet`` property
as much as possible. In fact, there’s nothing specific about cats in
this class, so we might make our code a step more abstract and flexible
by doing the following:

.. code:: java

   public class PetOwner
   {
       private Feedable pet;

       public PetOwner(Feedable pet) {
           this.pet = pet;
       }

       public void feedThePet() {

           // ...code to prepare the pet's meal...

           pet.eat();
       }
   }

   public class CatOwner extends PetOwner
   {
       // code that requires Cat-specific behavior
   }

We’ve created a ``PetOwner`` class that encapsulates the behavior that
could apply to any pet (any ``Feedable``, actually), and have
``CatOwner`` extend ``PetOwner``. This allows other classes to extend
``PetOwner`` to make, say, a ``DogOwner`` that knows how to play fetch
with their pet, or a ``HorseOwner`` that knows how to ride their pet. It
also reduces the dependency of the ``feedThePet`` method on the specific
type of pet, since it doesn’t need to care.

To use this new class design, we can revise the sample code from above
as follows:

.. code:: java

   HouseCat suki = new HouseCat("Suki", 12);
   CatOwner Annie = new CatOwner(suki);

   Annie.feedThePet();

While the code usage here remains unchanged except for changing the
method name from ``feedTheCat`` to the more generic ``feedThePet``, the
opportunities for using the classes we’ve built are much wider since the
defined classes are no longer dependent on the specific ``Cat`` class.
Also notice that we’ve used the object ``suki`` in a polymorphic way,
creating it as a ``HouseCat``, but using it as a ``Feedable`` within the
``CatOwner`` class.

.. raw:: html

   <aside class="aside-note">

Like inheritance, interfaces enable polymorphic usage of objects. We can
create an object, and then use it in different contexts based on any
interfaces that it implements.

.. raw:: html

   </aside>

One final note before discussing how we might use interfaces in our
code: *Interfaces may not be created like objects are, with* ``new``.
You may implement an interface, or declare variables and parameters as
interface types. You can not, however, create an instance of an
interface.