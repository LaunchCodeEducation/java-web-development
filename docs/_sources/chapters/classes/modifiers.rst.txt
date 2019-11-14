Modifiers in Java
=================

.. index:: ! access level, ! access modifier, ! public, ! private, ! default access

.. _access-modifiers:

Access Modifiers
----------------

For fields in classes, the **access level** determines who can get or set
the value of the field. For methods, the **access level** determines who can
call the method. The access level of a class member is determined by an
**access modifier**.

We’ve encountered access modifiers so far in our code. In our examples, you
frequently see the keyword, ``public``. ``public`` makes the field or method to
be accessible by anyone working with our code. Another common access modifier
is ``private``, which restricts access to fields or methods so they can only be
used within the class. Two additional access modifiers are available in Java,
though they are used much less often than ``public`` and ``private``.

.. admonition:: Example

   Let's take another look at our ``HelloWorld`` class from the last section,
   but with one small change.

   .. sourcecode:: java
      :linenos:

      public class HelloWorld {

         String message = "Hello World";

         void sayHello() {
            System.out.println(message);
         }

      }

   In this ``HelloWorld`` class, we omit the ``public`` access modifier in lines
   3 and 5. Doing this implicitly gives the message field and the ``sayHello``
   method **default access**.

We should avoid giving everything default access when creating classes in Java
and instead think carefully about what level of access each field and method
should have.

The table below details whether or not information can be accessed at different
levels based on the access modifier. For example, a field with the ``private``
access modifier can be accessed within the class, but cannot be accessed
outside the class at the world-level. In Java, world-level is the level of the
whole application and contains all of the packages and classes. While we will
discuss later how to decide which access modifier to use for different
scenarios, you should save this table now as reference for those conversations.

.. list-table:: Is information accessible at certain levels with certain access modifiers?
   :widths: auto
   :header-rows: 1

   + - Modifier
     - Class
     - Package
     - World
   + - ``public``
     - Yes
     - Yes
     - Yes
   + - ``protected``
     - Yes
     - Yes
     - No
   + - (no modifier, aka *package-private* or *default*)
     - Yes
     - Yes
     - No
   + - ``private``
     - Yes
     - No
     - No

.. note::

   If you would like to learn more about access modifiers, you should check out the `Oracle documentation <https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html>`_ on the subject.

Let's take a look at our ``HelloWorld`` class again and add some access
modifiers.

.. admonition:: Example

   .. sourcecode:: java
      :linenos:

      public class HelloWorld {

         private String message = "Hello World";

         public void sayHello() {
            System.out.println(message);
         }

      }

Since ``message`` only needs to be used by ``sayHello``, we declare it to be
``private``. Since we want ``sayHello`` to be usable by anybody else, we
declare it to be ``public``.

.. admonition:: Note

   In Java, you should always use the most restrictive access modifier
   possible. Minimizing access to class members allows code to be
   refactored more easily in the future, and hides details of how you
   implement your classes from others.

   This makes your code more modular and modifiable. Each public member
   that you expose is another field or property that can be referenced
   directly elsewhere in any program using your class. Thus, changing any
   such field in your code could potentially break any code referencing
   such members. The fewer public members, the more you can change your
   code without breaking stuff elsewhere.

.. admonition:: Note

   If you want to learn more about controlling access to members of a class, check
   out this information from
   `Oracle <https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html>`__.

Check Your Understanding
------------------------

.. admonition:: Question

   For this question, refer to the code block below.

   .. sourcecode:: java

      public class Greeting {

         String name = "Jess";

         public void sayHello() {
            System.out.println("Hello " + this.name + "!");
         }
      }

   What access modifier would you give ``name``?

   a. no access modifier
   b. ``public``
   c. ``private``
   d. ``protected``

.. ans: B, private.


