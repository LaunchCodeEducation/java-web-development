Interfaces and Abstract Classes
===============================

We mentioned previously that interfaces share some characteristics with
abstract classes. Recall that an abstract class is one declared with the
``abstract`` keyword. You may not create an object from an abstract
class, and like an interface, an abstract class is allowed to contain
methods that only have signatures (that is, they don’t have
implementation code).

The main differences between interfaces and abstract classes are:

#. You *implement* an interface, while you *extend* an abstract class. The net effect of this is that a class may implement interfaces while also extending a class. Note that while you can implement *more than one* interface, you can only extend *one* class.
#. Abstract classes may contain non-constant fields, while interfaces can only contain constant fields.
#. Interfaces may only contain implementation code inside of default or static methods. Therefore, interfaces can’t contain methods that need to be shared by class instances in the same way that abstract classes do. In particular, any method that needs to use an instance property may not be part of an interface, since interfaces don’t have instance properties. Unlike interfaces, abstract classes may have methods which are not static or default and which do have instance properties. 
   
*We should use abstract classes to collect and specify behavior by related classes, while we should use an interface to specify related behaviors that may be common across unrelated classes.*

.. admonition:: Example

   Let's go back to our ``Feedable`` interface. If we want to add a ``Dog`` class to our application, we might implement the ``Feedable`` interface for our ``Dog`` class.
   This makes sense as dogs are creatures that we feed. However, as dogs and cats are so different, it is unlikely that they would share many behaviors through the ``Pet`` class.

Check Your Understanding
------------------------

.. admonition:: Question

   Check all statements that are TRUE about the differences between interfaces and abstract classes.

   a. You extend an abstract class, but implement an interface.
   b. You can implement many interfaces and many classes.
   c. Interfaces cannot contain non-constant fields, but abstract classes can.
   d. Methods that use instance properties can be in both interfaces and abstract classes.

.. ans: a,c
