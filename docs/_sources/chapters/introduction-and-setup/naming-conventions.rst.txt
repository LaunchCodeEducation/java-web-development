.. _naming-conventions:

Java Naming Conventions
=======================

Java has some very straightforward naming conventions. These are
universally used by Java programmers, and differ in some cases from
conventions commonly used in other languages.

Again, these are conventions. Ignoring them will not prevent your code from running, 
as long as you are following Java’s `naming
rules <http://docs.oracle.com/javase/specs/jls/se8/html/jls-3.html#jls-3.8>`__. Java’s 
identifier naming rules are somewhat hard to parse, so a good
rule-of-thumb is that you should use only letters, numbers, and the
underscore character ``_``, and they should always start with a letter.

The naming conventions are more like guidelines than rules and are what other Java coders 
expect to see when reading your code.

.. list-table::
   :header-rows: 1

   * - Identifier Type  
     - Convention
     - Examples

   * - Package
     - All lowercase
     - ``demos.javawebdevelopment``,  ``org.launchcode.utilities``

   * - Class
     - Start with an uppercase letter
     - ``Scanner``, ``System``, ``Cello`` 

   * - Method
     - Start with a lower case letter, and use camelCase to represent multi-word method names 
     - ``nextInt()``, ``getId()`` 

   * - Instance variable
     - Start with a lowercase letter and use camelCase 
     - ``id``, ``firstName``

   * - Constant
     - All uppercase letters, words separated by underscores 
     - ``MAX_INT``

.. note::

   Constants in Java are variables created using both ``static`` and
   ``final`` modifiers. For example: ``static final Double PI = 3.14159``

.. tip::

   If you're not sure about all of these identifier types yet, that's ok. Keep
   this page in mind for future reference as you read through this book.

Oracle, the company that develops the Java language, provides some `more
detailed naming
conventions <http://www.oracle.com/technetwork/java/codeconventions-135099.html>`__.
(From the date on this article, you’ll note that these have been
relatively standard for a very long time!)
