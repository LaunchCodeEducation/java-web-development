Model-Binding
=============

.. index:: ! model binding

With a separate data layer implemented and items being tracked with unique
identifiers, we have the elements in place to auto-create model instances
with a technique called **model binding**. Model binding takes place when a whole 
model object is created on form submission. This saves us the effort, and the code, to 
pass in each form field to a controller. 

Remember how we want to be able to remove an event? With model binding we will
now be able to make it happen. Model binding reduces the amount of code we need to 
write to create an object and it helps with validation (which we’ll explore further in the next
section). Because we use the ``@ModelAttribute`` annotation, Spring Boot
will create an ``Event`` object for us when it gets the ``POST``
request from ``/create``.

How to Use Model-Binding - Video
--------------------------------

.. todo:: Add model video #2 here...

How to Use Model-Binding - Text
--------------------------------

With ``Event`` model in place, we can incorporate another annotation, ``@ModelAttribute``
When submitting the event creation information, rather than passing in each field used to 
instantiate a model, we can instead pass in ``@ModelAttribute Event newEvent`` as a parameter 
of the controller method. This technique is called model binding. The Model instance is created
on form submission. 

With this in mind, we need to return to the create form HTML and update the form fields to
match the event object property names. 

Check Your Understanding
-------------------------

.. admonition:: Question

   Complete this sentence: Model binding ...

   #. requires ``@ModelAttribute`` annotation.
   #. helps with form validation.
   #. reduces controller code.
   #. All of the above. 

.. ans: d, all of the above.
