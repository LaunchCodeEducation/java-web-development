Types of Relationships
======================

Just as data in different database tables :ref:`can have relationships <one-to-many-sql>` to each other, so can classes and objects. In fact, relationships between objects will translate into relationships between rows in a database when using an ORM tool. 

This chapter introduces the tools needed to create meaningful relationships using an ORM tool. Before diving in, however, let's consider the different types of relationships at a conceptual level. 

To illustrate the different types of relationships, we will refer to types, or classes, using capital letters A and B. Instances of these types will be denoted a\ :sub:`1`, a\ :sub:`2`, a\ :sub:`3` for elements of type A and b\ :sub:`1`, b\ :sub:`2`, b\ :sub:`3` for elements of type B.

One-to-One
----------

.. index:: ! one-to-one

The simplest type of relationship is the **one-to-one relationship**. This occurs when each instance of type A may be related to only one instance of type B, and vice versa.

.. todo:: insert one-to-one diagram

.. admonition:: Examples

   The following pairs of things generally have one-to-one relationships:

   #. People / driver's licenses
   #. States / capital cities
   #. iPhones / serial numbers

.. admonition:: Note

   It is not *required* that each instance of type A be related to an instance of type B. For example, a person may not have a driver's license.


One-to-Many and Many-to-One
---------------------------

.. index:: ! one-to-many

A **one-to-many** relationship occurs when each instance of type A may be related to more than one instance of type B, but each instance of B can only be related to a single instance of type A.

.. todo:: insert one-to-many diagram

.. index:: ! many-to-one

In this case, we say that A has a one-to-many relationship to B. When discussing the inverse relationship, we say that B has a **many-to-one** relationship to A.

.. admonition:: Examples

   The following pairs of things generally have one-to-many relationships:

   #. Birth dates / people
   #. U.S. Senators / states
   #. Model numbers / iPhones


Many-to-Many
------------

**Many-to-many** relationships occur when each instance of type A can be related to multiple instances of type B, and vice versa. 

.. todo:: insert many-to-many diagram

.. admonition:: Examples

   The following pairs of things generally have many-to-many relationships:

   #. Books / authors
   #. Recipes / ingredients
   #. Actors / movies
