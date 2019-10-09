Modifiers in Java
=================

Access Modifiers
----------------

For fields in classes, the access level determines who can get or set
the value of the field. For methods, the access level determines who can
call the method. The access level of a class member is determined by an
**access modifier**.

.. admonition:: Example

   Let's take a look at our ``HelloWorld`` class again.

   .. sourcecode:: java
      :linenos:

      public class HelloWorld {

         String message = "Hello World";

         void sayHello() {
               System.out.println(message);
         }

      }

   In declaring the ``message`` field and the ``sayHello`` method of
   our ``HelloWorld`` class, by omitting an access modifier we implicitly gave each
   **default access**.

We should avoid giving everything default access when creating classes in Java and instead think carefully about what level of access each field and method should have.

We’ve encountered access modifiers so far in our code. 
In our example above, you can see the keyword, ``public``.
``public`` makes the field or method to be accessible by anyone working with our code.
Another common access modifier is ``private``, which restricts access to fields or methods so they can only be used within the class.
Two additional access modifiers are available in Java, though they are used much less often than
``public`` and ``private``.

The table below details when different access modifiers are most appropriate. While we are introducing this concept now, later we’ll point out
specifically where different access modifiers might be useful when we encounter such scenarios.


.. list-table:: Access Modifiers
   :widths: auto
   :header-rows: 1

   + - Modifier
     - Class
     - Package
     - Subclass
     - World
   + - ``public``
     - Yes
     - Yes
     - Yes
     - Yes
   + - ``protected``
     - Yes
     - Yes
     - Yes
     - No
   + - (no modifier, aka *package-private* or *default*)
     - Yes
     - Yes
     - No
     - No
   + - ``private``
     - Yes
     - No
     - No 
     - No

.. note::

   If you would like to learn more about access modifiers, you should check out the `Oracle documentation <https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html>`_ on the subject.

Let's take a look at our ``HelloWorld`` class again and add some access modifiers.

.. admonition:: Example

   .. sourcecode:: java
      :linenos:

      public class HelloWorld {

         private String message = "Hello World";

         public void sayHello() {
            System.out.println(message);
         }

      }

Since ``message`` only needs to be used by ``sayHello``, we declare it to be ``private``.
Since we want ``sayHello`` to be usable by anybody else, we declare it to be ``public``.

.. note::

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


-  `Controlling Access to Members of a Class
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html>`__
-  `Using the this Keyword
   (docs.oracle.com) <https://docs.oracle.com/javase/tutorial/java/javaOO/thiskey.html>`__
