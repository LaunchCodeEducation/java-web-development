Old Java Curriculum: Encapsulating Behavior
============================================

Single Responsibility Principle
-------------------------------

As we wrap up our whirlwind tour of encapsulation, we want you think a
bit about how to go about building good classes. Doing so is more of an
art than a science, and it will take you lots of practice and time.
However, there are a few rules that we’ve pointed out to help guide you.
Here’s one more.

From
`Wikipedia <https://en.wikipedia.org/wiki/Single_responsibility_principle>`__:

.. raw:: html

   <aside class="aside-definition">

The **single responsibility principle** states that every module or
class should have responsibility over a single part of the functionality
provided by the software, and that responsibility should be entirely
encapsulated by the class.

.. raw:: html

   </aside>

It isn’t always clear what “responsibility over a single part of the
functionality” means. However, it is often very clear what it doesn’t
mean. For example, we wouldn’t think of adding functionality to the
``Student`` class that tracked all of the data for each of the student’s
classes, such as catalog number, instructor, and so on. Those are
clearly different areas of responsibility. One way to interpret the
Single Responsibility Principle is to say that “classes should be
small.”

As you go forth and create classes, the main thing to keep in mind is
that your skill and judgement in creating Java classes will improve over
time. The best way to improve is to write lots of code, ask lots of
questions, and continue learning!

References
----------

-  `Defining Methods
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/javaOO/methods.html>`__
-  `Passing Data to a Method or Constructor
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/javaOO/arguments.html>`__
-  `How to Implement Java’s equals Method
   Correctly <https://www.sitepoint.com/implement-javas-equals-method-correctly/>`__
-  `How to Implement Java’s hashCode
   Correctly <https://www.sitepoint.com/how-to-implement-javas-hashcode-correctly/>`__
-  `Single Responsibility
   Principle <https://en.wikipedia.org/wiki/Single_responsibility_principle>`__
