Model-Binding
=============

.. index:: ! model binding

With a separate data layer implemented and items being tracked with unique
identifiers, we have the elements in place to auto-create model instances
with a technique called **model binding**. Model binding takes place when a whole 
model object is created on form submission. This saves us the effort, and the code, to 
pass in each form field to a controller. 

Model binding reduces the amount of code we need to 
write to create an object and it helps with validation (which we’ll explore further in the next
section). Because we use the ``@ModelAttribute`` annotation, Spring Boot
will create an ``Event`` object for us when it gets the ``POST``
request from ``/create``.

How to Use Model-Binding - Video
--------------------------------

.. todo:: Add model video #2 here...

How to Use Model-Binding - Text
--------------------------------

.. index:: ! @ModelAttribute

With ``Event`` model in place, we can incorporate another annotation, ``@ModelAttribute``
When submitting the event creation information, rather than passing in each field used to 
instantiate a model, we can instead pass in ``@ModelAttribute Event newEvent`` as a parameter 
of the controller method. 

Revised ``processCreateEventForm`` in ``EventController``:

.. sourcecode:: java
   :lineno-start: 32

   @PostMapping("create")
   public String processCreateEventForm(@ModelAttribute Event newEvent) {
      EventData.add(newEvent);
      return "redirect:";
   }

This is the essence of model binding. The model instance is created
on form submission. With only two fields needed to create an event, the value of this data binding may not be
particularly apparent right now. You can imagine, though, with a larger form, that ``@ModelAttribute`` is quite an 
efficient annotation.

Another benefit of model binding is that we can use the model field names as the form field names. So back in 
the create form HTML, we will update the form fields to match the event fields. 

``events/create.html``:

.. sourcecode:: html
   :lineno-start: 9

   <div class="form-group">
      <label>Name
         <input type="text" name="name" class="form-control">
      </label>
      <label>
         Description
         <input type="text" name="description"  class="form-control">
      </label>
   </div>   

Check Your Understanding
-------------------------

.. admonition:: Question

   Complete this sentence: Model binding ...

   #. requires ``@ModelAttribute`` annotation.
   #. helps with form validation.
   #. reduces controller code.
   #. All of the above. 

.. ans: d, all of the above.
