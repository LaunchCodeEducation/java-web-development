Creating a One-to-One Relationship
==================================

We :ref:`defined a one-to-one relationship <one-to-one-def>` between two objects, A and B, as occurring when an object of type A can be related to only one instance of an object of type B, and vice versa.

Such a relationship can be configured using the JPA annotation ``@OneToOne``.

Creating a One-to-One Relationship - Video
------------------------------------------

.. raw:: html

   <div style="text-align:center;"><iframe width="800" height="450" src="https://www.youtube.com/embed/0yNIbAcd4ng" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

The final code from this video is in the `one-to-one branch <https://github.com/LaunchCodeEducation/coding-events/tree/one-to-one>`__ of ``coding-events``.

Creating a One-to-One Relationship - Text
-----------------------------------------

The ``EventDetails`` Class
^^^^^^^^^^^^^^^^^^^^^^^^^^

Relating ``EventDetails`` to ``Event``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Cascading ORM Operations
^^^^^^^^^^^^^^^^^^^^^^^^

Template Updates
^^^^^^^^^^^^^^^^

The Inverse Relationship
^^^^^^^^^^^^^^^^^^^^^^^^

Once we have set up the relationship from ``Event`` to ``EventDetails`` it is easy to configure the inverse relationship.

To do so, add a field of type ``Event`` to ``EventDetails``. Then add ``@OneToOne`` to the new field with a ``mappedBy`` parameter.

.. sourcecode:: java

   @OneToOne(mappedBy = "eventDetails")
   private Event event;

Setting ``mappedBy = "eventDetails"`` will ensure that the field is populated correctly. For a specific ``EventDetails`` object ``details``, ``event`` will be populated with the ``Event`` object that contains ``details``. Then both sides of the one-to-one relationship will have a reference to the other.
