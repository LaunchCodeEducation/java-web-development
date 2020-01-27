Types of Relationships
======================

Just as data in different database tables :ref:`can have relationships <one-to-many-sql>` to each other, so can classes and objects. In fact, relationships between objects will translate into relationships between rows in a database when using ORM. 

This chapter introduces the tools needed to create meaningful relationships using ORM. Before considering how to do this with Spring Boot, however, let's consider the different types of relationships at a conceptual level. 

For the examples below, we use four classes:

- ``Event`` - A class representing a coding event.
- ``EventCategory`` - A class representing categories of coding events.
- ``EventDetails`` - A class that encapsulates details about a single event, such as description, contact email, location, and so on.
- ``Tag`` - A piece of metadata labeling an event. You can think of these as topics that an event might include, such as Java, Spring, or JavaScript. An event can cover multiple topics, so it can have multiple tags.

The first two of these are familiar to you from our ``coding-events`` app. The ``EventDetails`` and ``Tag`` classes will be introduced later in this chapter.

.. _one-to-one-def:

One-to-One
----------

.. index:: ! one-to-one

The simplest type of relationship is the **one-to-one relationship**. This occurs when each instance of type A may be related to only one instance of type B, and vice versa.

.. admonition:: Note

   In the following examples, arrows point in the direction of the relationship. If A points to B, then you can say that A *knows about* B.

   While relationships in SQL are bidirectional, relationships in programming languages are unidirectional. In other words, if A knows about B, then B doesn't necessarily know about A.

.. figure:: figures/one-to-one.png
   :alt: A single Event object on the left, with a double-sided arrow point to a single EventDetails object on the right
   :width: 800px

   A one-to-one relationship between an ``Event`` object and an ``EventDetails`` object

An ``Event`` object should only have one collection of details, so it should only be related to one ``EventDetails`` object. Similarly, details about an event are specific to that event, so an ``EventDetails`` object should only be related to one ``Event`` object.

.. admonition:: Examples

   The following pairs of things generally have one-to-one relationships:

   #. People / driver's licenses
   #. States / capital cities
   #. iPhones / serial numbers

   It is not *required* that each instance of type A be related to an instance of type B. For example, a person may not have a driver's license.

One-to-Many and Many-to-One
---------------------------

.. index:: ! one-to-many

A **one-to-many** relationship occurs when each instance of type A may be related to more than one instance of type B, but each instance of B can only be related to a single instance of type A.

.. figure:: figures/one-to-many.png
   :alt: A single EventCategory object on the left, related to two Event objects on the right
   :width: 800px

   A one-to-many relationship between ``EventCategory`` and ``Event`` objects

.. index:: ! many-to-one

In this case, we say that A has a one-to-many relationship to B. A category can contain multiple items, therefore an ``EventCategory`` object may be related to multiple ``Event`` objects. But an event may only be in one category.

.. admonition:: Examples

   The following pairs of things generally have one-to-many relationships:

   #. Birth dates / people
   #. States / U.S. Representatives
   #. Model numbers / iPhones

When discussing the inverse relationship, we say that B has a **many-to-one** relationship to A.

.. figure:: figures/many-to-one.png
   :alt: Two Event objects on the left, related to a single EventCategory object on the right
   :width: 800px

   A many-to-one relationship between ``Event`` and ``EventCategory`` objects

A many-to-one relationship operates in the opposite direction of a one-to-many relationship. The difference between the two is which side of the relationship *knows about* the objects on the other side. In Java terms, this will translate into a field on one class that references the other.

.. admonition:: Examples

   Many-to-one relationships are simply the opposite direction of one-to-many. Therefore, each of the following pairs has a many-to-one relationship.

   #. People / birth dates
   #. U.S. Representatives / states
   #. iPhones / model numbers


Many-to-Many
------------

**Many-to-many** relationships occur when each instance of type A can be related to multiple instances of type B, and vice versa. 

.. _many-to-many-figure:

.. figure:: figures/many-to-many.png
   :alt: Three Event objects on the left, with various relationships to three Tag objects on the right
   :width: 800px

   A many-to-many relationship between Event and Tag objects

An event can have multiple tags, and a tag may be associated with multiple events. Thus, we have a many-to-many relationship.

.. admonition:: Examples

   The following pairs of things generally have many-to-many relationships:

   #. Books / authors
   #. Recipes / ingredients
   #. Actors / movies

Check Your Understanding
------------------------

.. admonition:: Question

   Match the following pairs with the appropriate relationship type:

   #. car / manufacturer
   #. car / title
   #. car / driver 
   #. car / tire

.. ans: a. many-to-one, b. one-to-one, c. many-to-many, d. one-to-many

.. admonition:: Question

   True/False: In order for two Java classes, A and B, to be mapped in a one-to-many relationship, class A must 
   contain a field for instances of B and B must have a field for instances of A.

   #. True
   #. False

.. ans: False, A one-to-many relationship may be present without B containing a field A.

