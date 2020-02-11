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

The flow of this request can be described as follows:

#. Server receives ``POST`` request
#. Server creates ``newEvent`` object using request parameters
#. ``processCreateEventForm`` is called with ``newEvent``
#. ``newEvent`` is saved
#. A 303 redirect response is returned, redirecting the user to ``/events``

The request creates an ``Event`` object using data from the incoming request. Regardless of what the data looks like, the new object is saved to the data layer. The user could submit an empty form, with no name or description filled in, and our code would be happy to create an ``Event`` and save it. Similarly, a user could submit the full text of the massive novel "War and Peace" as the description. This isn't great. 

.. admonition:: Note

   Technically, submitting a request containing "War and Peace" would fail with most applications. This is because web servers typically set a limit on the maximum size of a ``POST`` request. However, our application code is willing to take requests of any size, at this point.


Some modest validation rules for a new ``Event`` object might be:

- The ``name`` field must contain between 3 and 20 characters, and 
- The ``description`` field may be empty, but may contain no more than 500 characters.

With these rules in place, conceptually, the flow of our controller code should look more like the following:

#. Server receives ``POST`` request
#. Server creates ``newEvent`` object using request parameters
#. ``processCreateEventForm`` is called with ``newEvent``
#. **Controller checks for validation errors in the model object. If errors are found, return the user to the form. Otherwise, proceed.**
#. ``newEvent`` is saved
#. A 303 redirect response is returned, redirecting the user to ``/events``

Let's look at how we can practically do this within Spring Boot.

Handling Validation Errors - Video
----------------------------------

.. youtube::
   :video_id: omSQO6721cU
   :gh_path: LaunchCodeEducation/coding-events/validation-errors

Handling Validation Errors - Text
----------------------------------

When using model binding, we can use Spring Boot annotations and tools to validate new model objects before they are saved to a data layer or database. 

Using ``@Valid``
^^^^^^^^^^^^^^^^

Within ``EventController``, the ``processCreateEventForm`` handler method uses model binding to receive an ``Event`` object that is created using form data. This object is NOT validated automatically, even if validation annotations are present on its fields.

Recall that *both* the model and controller play a role in validation. The model's responsibility is simply to define validation rules. The controller must check that those rules are satisfied.

The first step to enable validation in a controller is to add ``@Valid`` to a method parameter that is created using model binding. 

.. sourcecode:: java

   @PostMapping("create")
   public String processCreateEventForm(@ModelAttribute @Valid Event newEvent) {
      EventData.add(newEvent);
      return "redirect:";
   }

In lieu of explicit validation error handling (which we will cover below), Spring Boot throws an exception if validation fails for the new object. This means that an object that fails validation will NOT be saved. 

.. figure:: figures/validation-exception.png
   :alt: An exception is thrown if @Valid is applied without explicit handling of validation errors.

   A validation exception displayed in the browser

However, the user experience for this flow is not great. If a user submits bad data, rather than showing them a complicated stack trace, we would be better off to provide a helpful message and allow them to try again.

.. admonition:: Note

   Remember, exceptions should be messages to programmers and programs, not end users. Even if an exception occurs, we should avoid displaying it to the user.

Using the ``Errors`` Object
^^^^^^^^^^^^^^^^^^^^^^^^^^^

We can prevent a validation exception from being thrown by explicitly handling validation errors. Spring Boot makes an object of type ``Errors`` available when a method uses ``@Valid``. As with ``Model`` objects, we can access this object by placing it in a method's parameter list. 

.. sourcecode:: java
   :lineno-start: 33

   @PostMapping("create")
   public String processCreateEventForm(@ModelAttribute @Valid Event newEvent,
                                       Errors errors, Model model) {
      if(errors.hasErrors()) {
         model.addAttribute("title", "Create Event");
         model.addAttribute("errorMsg", "Bad data!");
         return "events/create";
      }

      EventData.add(newEvent);
      return "redirect:";
   }

Here, we have added ``Errors errors`` to our handler. This object has a boolean method, ``.hasErrors()`` that we can use to check for the existence of validation errors. If there are validation errors, we return the form again, along with a simple message for the user. This message can be displayed in the ``events/create`` template by adding some code above the form:

.. sourcecode:: html

   <p th:text="${errorMsg}" style="color:red;"></p>

Now, when a user submits the form with bad data they will be notified and no exception will be thrown. However, the message "Bad data!" is far from ideal. The next section introduces a technique to display more useful error messages. 

Check Your Understanding
------------------------

.. admonition:: Question

   Which of the following statements are true?

   #. A method parameter may have only one annotation.
   #. ``@Valid`` can only be used in conjunction with model binding.
   #. Using ``@Valid`` means that a method will never be called with invalid data.
   #. Spring Boot can infer validation requirements based on the name of a field. 

.. ans: b, @Valid can only be used in conjunction with model binding.
