Studio: Spinning the Discs
===========================

Although they look the same, the old optical discs---CDs and DVDs---are quite
different from each other. Let's use them as the focus for creating a new
interface.

Getting Ready
--------------

Set up a local copy of the project:

#. Visit the `repository page <https://github.com/LaunchCodeEducation/java-web-dev-studio7>`__
   for this project and fork it to create a copy under your own GitHub account.
#. Back in IntelliJ, close any open projects.
#. On the IntelliJ welcome screen, click *Check out from Version Control* and
   select *Git*.
#. Choose your fork from the repository dropdown, select the parent directory
   where you'd like to store your project, and hit *Clone*.
#. In the first modal screen, select *Create project from existing sources*.
   Accept the default settings on all other screens.

Disc Project Overview
----------------------

In this activity, you will pair up to design a new custom interface.

Take a look at the prepared ``CD`` and ``DVD`` classes in the starter
code---only their signatures are present. You will add fields and methods by
extending a base class and implementing your interface. Before you do this,
however, you need to consider what code to place in the interface vs. the
abstract class vs. each specific class.

Just like you did with your Restaurant Menu studios, you will begin with pen
and paper (or similar tools).

Consider Generic Behaviors
---------------------------

Here are a few behaviors that both CDs and DVDs share:

a. They both spin,
b. They both store data,
c. Data gets written to the discs by using a laser,
d. The data on the discs can be read by using a laser,
e. Once loaded, they both report information like name, capacity, contents, and
   disc type.

With your partner, add one or two more behaviors to the list. Feel free to
do some quick research online if needed. Note that information like storage
capacity does NOT belong on this list, since it describes a *property*
(field) rather than a *behavior* (method).

For each behavior, identify if it depends on any type of instance variable.
For example, the spinning behavior does not require any field information
from the ``CD`` or ``DVD`` classes.

This collecting and sorting of behaviors is the first step toward designing
your interface and abstract class. It prompts you to consider behaviors that
can be generally applied vs. those that depend on data stored in a specific
object.

Consider Class-Specific Behavior and Data
------------------------------------------

Next, you and your partner need to decide which behaviors go into the
interface vs. an abstract class.

Behaviors added to an interface do NOT have to be identical for every object
that implements the interface. The key is that the methods require no
object-specific data. The methods can accept parameters, but these should
represent generic values like ``String searchTerm`` rather than field data
like ``DVD.title``.

For example, even though CDs and DVDs both spin, they do so at different
speeds. Their *behavior* (spinning) is the same, but the details of that
behavior vary. Thus, a method like ``spinDisc()`` fits well into an interface.

#. For the other behaviors you and your partner sorted, decide which ones
   belong in the interface.
#. Write down details about how these behaviors differ for CDs and DVDs. This
   guides your thinking about how each class should override the methods.
#. For the behaviors that cannot go into the interface, decide if they could be
   placed in an abstract class or if they need to appear in the separate ``CD``
   and ``DVD`` classes.
#. Finally, write down the fields needed to define the properties of a CD or
   DVD (e.g. ``storageCapacity``). Consider:

   a. Which fields are shared by both types of discs, and which ones are
      unique to each class?
   b. Do any of the fields represent *constants*?

Code the Interface
-------------------

Now that your team has completed the before-coding thinking, it's time to
start building!

#. Add an ``OpticalDisc`` file for the interface. Refer back to
   :ref:`Creating an Interface <create-an-interface>` if you need a quick
   review of the syntax.
#. Declare and initialize any constant fields.
#. Add a method signature for each of the behaviors you identified for the
   interface. For example:

   .. sourcecode:: java

      void spinDisc();

Good work. Now you need to step back from the interface for a moment and take
care of the remaining methods and fields.

Code the Abstract Class
------------------------

To streamline the field and constructor code for ``CD`` and ``DVD``, you
need to start with a base class.

#. Create an abstract ``BaseDisc`` class and declare the fields used by both
   ``CD`` and ``DVD``.
#. Code the shared constructors, getters, setters, and custom methods.

OK. Now put your code to work.

Complete the Disc Classes
--------------------------

#. Extend the base class into the ``CD`` and ``DVD`` classes.
#. Implement the interface in each class.
#. Fill in the ``@Override`` code for each of the interface methods.

   .. admonition:: Tip

      You can hover over the ``implements`` keyword and click the IntelliJ
      suggestions to generate these method signatures.

      Since these are *signatures* only, you will need to add specific code to
      each method.

#. Add getters, setters, and any other custom methods needed by each class.

Add Method Calls to ``Main``
-----------------------------

In the ``main`` method, declare and initialize a ``CD`` and ``DVD`` object,
then run each of the behaviors you and your partner identified.

.. admonition:: Example

   .. sourcecode:: java
      :linenos:

      myCd.spinDisc();
      myDvd.spinDisc();

   **Output**

   .. sourcecode:: Bash

      A CD spins at a rate of 200 - 500 rpm.
      A DVD spins at a rate of 570 - 1600 rpm.

Bonus Missions: Other Discs & Disks?
-------------------------------------

#. CDs and DVDs are not the only flat, circular media that have been used to
   store and return data.

   a. Add classes for vinyl records (LPs) and floppy disks.
   b. Does your interface apply to all four classes? If so, implement the
      interface into the LP and floppy classes, and complete the appropriate
      override methods.
   c. If your interface does NOT apply to all of the classes, modify it to do so.
      (Note: At the very least, you need to rename the interface).
   d. Does your abstract class apply to LPs and floppy disks? If so, extend it
      into the new classes. If not, should you modify it or extend a
      *different* abstract class?

#. What about wheels and Frisbees? These are also spinning disks, but they are
   not used for data storage.

   a. Abstract class or interface? Which one can be applied to the ``Wheel``
      and ``Frisbee`` classes?
   b. Discuss these questions with your peers, then code one of the classes
      just for fun.
