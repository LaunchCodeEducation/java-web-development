Model Data 
==========

In order to work with data, we need to add another element to our MVC application. Say for example,
we want to do things like remove an event from our list. Well, if two events both have the same name, 
how might we identify which of those items to delete? We can't yet. So we need to tweak how we store
event data. 

In ``coding-events``, we add a unique identifier field to ``Events`` to better handle distinct ``Event`` 
instances. We'll also create another model class called ``EventData`` to encapsulate data storage and prepare
ourselves for decoupling data from model classes.

Add a Unique Id - Video
-----------------------

.. todo:: video adding a unique id generator

Add a Unique Id - Text
-----------------------

Identifying data by a string ``name`` is not a sustainable or scalable method
of handling data in most situations. Consider the address book example. How can
we distinguish between two contact entries with the same name field? It is a frequent
practice to add a unique id field to a class responsible for modelling data. This ensures
that our address book can contain two separate entries for our friends who have the same 
name as one another. 

Add an ``id`` field to the ``Event`` model class. Create a static counter method that will increase the value
of the event field each time a new instance is created, thus producing a unique id for each ``Event`` object.
Create a constructor that sets ``id`` using this method and calls the default, no-arg constructor.

Create a Data Layer - Video
---------------------------

.. todo:: video showing creation of EventData class

Create a Data Layer - Text
--------------------------

Now that we've begun building a model, it's a good time to remind ourselves that models are not designed to be 
data storage containers. Rather, models are meant to shape the data stored in another location into objects that 
can be used in our application. As we work our way into learning about database usage and service calls, however, 
we'll use a model to store some data temporarily. 

Create a new package called ``data`` and add a class ``EventData``. Whereas ``Event`` is responsible for organizing
user-inputted information into a Java object, ``EventData`` is responsible for maintaining those objects once they 
are created. ``EventData`` is itself a Java class that stores events. It can add events with an
``add`` method, ``getById``, ``getAll``, and ``remove``. 

With ``EventData`` managing event data, we must once again refactor ``EventController`` to update the items stored in 
``EventData``.

Delete an Event - Video
-----------------------

.. todo:: video showing event deletion

Delete an Event - Text
----------------------

Now that we've refined our events storage method, we are able to tackle the task of deleting an object. 
To delete an event object from storage, we'll grab the event's id and use that
information to call the ``remove`` method.
Since the delete event is user-initiated, a controller will be involved to pass
the information from the user-accessible view to the data layer. So our first step
with this task is to create a controller method to get a view to delete events.
Thus, we'll also be creating a new view by adding a new template, ``events/delete.html``.
This view will need to reference event IDs in order to do its job. 

We also need a POST handler to take care of what to do when the delete event information
is submitted by the user. We'll have this post handler redirect the user back to the home 
page once they have selected which event or events to remove from storage.
Like the rest of the templates, the delete form view should include the header fragment.


Check Your Understanding
-------------------------

Questions here...
