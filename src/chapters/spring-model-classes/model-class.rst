Create a Model
==============

The first step to moving data out of controller classes is to actually create a model class.
As we discussed on the previous page, the controller class is not responsible for holding data.
In ``coding-events``, we'll remove the HashMap data from ``EventController`` and create a proper 
Java class to deal with event items. We'll then update our controller methods to take
advantage of the new model and it's properties, rather than the strings stored in the HashMap.
Lastly, because the controller is updating, the template variables it relies upon will also need to
change to reflect the model properties.

Create a Model Class - Video
----------------------------

.. todo:: video showing model creation

Create a Model Class - Text
---------------------------

.. index:: ! POJO

Like controllers, model classes are conventionally located in a ``models``
package. Structurally, model classes most closely resemble the kinds of classes we practiced
making at the start of this course, before introducing Spring Boot. In other words,
models are *plain old Java objects*, or POJOs.

To create a model to shape event data, we'd want to include fields for the ``name`` and ``description``.
Of course, we'll also like some constructors and getters and setters. 

Now that we're working to move the data handling out from the controller classes and into a class of its own, we'll
need to update the post handler that creates new event objects. 

Back in the ``events/index.html`` template, update the HTML to use the ``Event`` object's fields, rather than simply strings.

.. admonition:: .. note:: 

	The syntax ``event.fieldName`` runs a getter method behind the scenes in order to access a field name.

Add a Model Property - Video
----------------------------

.. todo:: video adding a property to the model class

Add a Model Property - Text
---------------------------

Add a ``description`` field to the ``Event`` model class. Update both the ``events/create.html`` and ``events/index.html``
templates to create an event object with a description field and to display that description along with the event's 
name. Lastly, add a parameter to the ``processCreateEventForm`` to handle the form submission and pass the description
value into the creation of the Event object.


Check Your Understanding
-------------------------

Questions here...

.. ## Create Model Class
- Create `models` package 
- Create `Event` class
- Refactor `processCreateEventForm` to create `Event` object
- Refactor `events/index` template to reference `Event` fields
- Test

.. ## Add Class Property
.. - Add `description` property to class
.. - Update `events/create` template to include description field
.. - Update `processCreateEventForm` to create object w/ description 
.. - Update `events/index` template to display description 

