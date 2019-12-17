.. _validating-models:

Validating Models in a Controller
=================================

Validation involves both model and controller components of an MVC application. After we have defined validation rules using annotations on the model, we must also update the controller to ensure that the rules are checked and appropriate action is taken when validation fails.

Validation Flow
---------------

Before diving into the details of the code, let's consider the logical flow of control for validating data in a request. Recall our ``POST`` handler from the previous chapter, which used model binding to create new ``Event`` objects from form submissions.

.. sourcecode:: java

   @PostMapping("create")
   public String processCreateEventForm(@ModelAttribute Event newEvent) {
      EventData.add(newEvent);
      return "redirect:";
   }

The flow of this request can be described like this:

#. Server receives ``POST`` request
#. Server creates ``newEvent`` object using request parameters
#. ``processCreateEventForm`` is called with ``newEvent``
#. ``newEvent`` is saved
#. A 303 redirect response is returned, redirecting the user to ``/events``

The request creates an ``Event`` object using data from the incoming request. Regardless of what the data looks like, the new object is "saved" to the data layer. The user could submit an empty form, with no name or description filled in, and our code would be happy to create an ``Event`` and save it. Similarly, a user could submit the full text of the massive novel "War and Peace" as the description. This isn't great. 

.. admonition:: Note

   Technically, submitting a request containing "War and Peace" would fail with most applications. This is because web servers typically set a limit on the maximum size of a ``POST`` request. However, our application code is willing to take requests of any size, at this point.


Some modest validation rules for a new ``Event`` object might be:

- The ``name`` field must contain between 3 and 20 characters, and 
- The ``description`` field may be empty, but may contain no more than 500 characters.

With these rules in place, conceptually, the flow of our controller code should look more like this:

The flow of this request can be described like this:

#. Server receives ``POST`` request
#. Server creates ``newEvent`` object using request parameters
#. ``processCreateEventForm`` is called with ``newEvent``
#. **Controller checks for validation errors in the model object. If errors are found, return the user to the form. Otherwise, proceed.**
#. ``newEvent`` is saved
#. A 303 redirect response is returned, redirecting the user to ``/events``

Let's look at how we can practically do this within Spring Boot.

Handling Validation Errors - Video
----------------------------------

.. raw:: html

   <div style="text-align:center;"><iframe width="800" height="450" src="https://www.youtube.com/embed/omSQO6721cU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

The final code from this video is in the `validation-errors branch <https://github.com/LaunchCodeEducation/coding-events/tree/validation-errors>`__ of ``coding-events``.

Handling Validation Errors - Text
----------------------------------

Using ``@Valid``
^^^^^^^^^^^^^^^^

Using the ``Errors`` Object
^^^^^^^^^^^^^^^^^^^^^^^^^^^
