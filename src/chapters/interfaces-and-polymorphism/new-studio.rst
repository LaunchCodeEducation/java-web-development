Studio: Spinning the Discs
===========================

Although they look the same, the old optical discs---CDs and DVDs---are quite
different from each other. Let's use them as a model for creating a new
interface.

Getting Ready
--------------

   TODO: Add link to starter code repository.

Set up a local copy of the project:

#. Visit the repository page (*TODO: Add link here*)
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

Lorem ipsum...

Consider Generic Behaviors
---------------------------

Some intro text here...

#. With a partner, start by making a list of behaviors that both CDs and DVDs
   share (e.g. they spin).
#. Next, sort the behaviors according to whether or not they depend on
   any type of instance variable.
#. If ALL of the behaviors you listed depend on instance data, then return to
   step 1. You can keep all of your current ideas, but focus on identifying
   at least one additional behavior that does NOT rely on a specific class
   field.
#. Next...

   Tie this work into starting the thought process behind what should go into
   the interface.

Consider Class-Specific Behavior and Data
------------------------------------------

Even though CDs and DVDs both spin, they do so at different speeds. Their
*behavior* (spinning) is the same, but the details of that behavior vary.

#. For the common behaviors you and your partner identified, provide details
   about how they differ for CDs and DVDs.
#. Next...

   Relate this section to thinking about how each class should override the
   interface methods.

Code the Interface
-------------------

Some transition text here...

#. Create an ``OpticalDisc`` file for the interface. Refer back to
   (*TODO: Add relevant chapter link*) if you need a quick review of how to do
   this.
#. Add a method signature for each of the common behaviors you identified. For
   example:

   .. sourcecode:: Java

      void spinDisc()

#. In the ``DVD`` and ``CD`` classes, implement the interface and fill in the
   override code for each of the interface methods.
#. Next...

Code the Abstract Class
------------------------

Lorem ipsum...

Bonus Missions: Other Discs & Disks?
-------------------------------------

#. CDs and DVDs are not the only flat, circular media that have been used to
   store and retrieve data.

   a. Add classes for vinyl records (LPs) and floppy disks.
   b. Does your interface apply to all four storage classes? If so, implement
      the interface into the LP and floppy classes, and complete the
      appropriate override methods.
   c. If your interface does NOT apply to all of the classes, modify it to do so.
      (Note: At the very least, you need to rename the interface).
   d. Does your abstract class apply to LPs and floppy disks? If so, extend it
      into the new classes. If not, should you modify it or extend a different
      abstract class?

#. What about wheels and Frisbees? These are also spinning disks, but they are
   not used for data storage.

   a. Abstract class or interface? Which one can be applied to the ``Wheel``
      and ``Frisbee`` classes?
   b. Next...
