Comparison to Abstract Classes
------------------------------

We mentioned above that interfaces share some characteristics with
abstract classes. Recall that an abstract class is one declared with the
``abstract`` keyword. You may not create an object from an abstract
class, and like an interface, an abstract class is allowed to contain
methods that only have signatures (that is, they don’t have
implementation code).

The main differences between interfaces and abstract classes are: - You
*implement* an interface, while you *extend* an abstract class. The net
effect of this is that a class may implement interfaces while also
extending a class. Note that while you can implement *more than one*
interface, you can only extend *one* class. - Abstract classes may
contain non-constant fields, while interfaces may not. - Interfaces may
only contain implementation code inside of default or static methods,
thus they can’t contain methods that need to be shared by class
instances in the same way that abstract classes do. In particular, any
method that needs to use an instance property may not be part of an
interface, since interfaces don’t have instance properties. Unlike
interfaces, abstract classes may have methods which are not static or
default and which do have implementation code. - Abstract classes should
be used to collect and specify behavior by related classes, while an
interface should be used to specify related behaviors that may be common
across unrelated classes.

For example, we could implement ``Comparator`` in many ways, to sort a
wide variety of classes whose objects may be compared to one another:
``Date`` (compare by temporal order), ``Student`` (compare by GPA),
``Person`` (compare by age), ``City`` (compare by population). However,
it’s unlikely that these classes would have any implementable behavior
that would warrant that they have the same base class.

