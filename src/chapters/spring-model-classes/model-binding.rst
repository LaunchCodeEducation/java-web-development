Model-Binding
=============

With a separate data layer implemented and items being tracked with unique
identifiers, we have the elements in place to auto-create model instances
with a technique called **model-binding**.

Remember how we want to be able to remove an event? With model binding we will
know be able to make it happen. Model binding reduces the amount of code we need to 
write to create an object and it helps with validation (which we’ll explore further in a future
lesson). Because we use the ``@ModelAttribute`` annotation, Spring Boot
will create an ``Event`` object for us when it gets the ``POST``
request from ``/add``.

How to Use Model-Binding - Video
--------------------------------

.. todo:: Add model video #2 here...

How to Use Model-Binding - Text
--------------------------------

With ``Event`` model in place, we can incorporate another annotation, ``@ModelAttribute``
When submitting the event creation information, rather than passing in each field used to 
instantiate a model, we can instead pass in ``@ModelAttribute Event newEvent`` as a parameter 
of the controller method. This techniquie is called model binding. The Model instance is created
on form submission. 

With this in mind, we need to return to the create form HTML and update the form fields to
match the event object property names. 

Check Your Understanding
-------------------------

Questions here...

.. ## Model Binding
- Modify `processCreateEventForm` to take `@ModelAttribute Event newEvent` parameter
- Update `events/create` so form fields match object property names 
- Test 
