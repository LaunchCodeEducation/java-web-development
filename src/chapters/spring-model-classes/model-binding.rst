Model-Binding
=============

.. index:: ! model binding

We now introduce a useful technique to auto-create model instances, 
called **model binding**. Model binding takes place when a whole 
model object is created by the Spring framework on form submission. This saves us the effort, and the code, needed to pass in each form field to a controller. 

Model binding reduces the amount of code we need to 
write to create an object and it helps with validation (which we’ll explore further in the next
section). Because we use the ``@ModelAttribute`` annotation, Spring Boot
will create an ``Event`` object for us when it gets the ``POST``
request from ``/create``.

How to Use Model-Binding - Video
--------------------------------

.. youtube::
   :video_id: gzk__EWfvaw
   :gh_path: LaunchCodeEducation/coding-events/model-binding

How to Use Model-Binding - Text
--------------------------------

.. index:: ! @ModelAttribute

With the ``Event`` model in place, we can incorporate another annotation, ``@ModelAttribute``.
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
particularly apparent right now. You can imagine, though, with a larger form and class, that ``@ModelAttribute`` is quite an 
efficient annotation.

For binding to take place, we must use the model field names as the form field names. So back in 
the create form HTML, we update the form fields to match the event fields. 

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

If a form field name does NOT match up with a model field, then binding will fail for that piece of data. It is critically important to ensure these names match up. 

Check Your Understanding
-------------------------

.. admonition:: Question

   Complete this sentence: Model binding ...

   #. requires an ``@ModelAttribute`` annotation.
   #. helps with form validation.
   #. reduces controller code.
   #. is useful for all of the reasons above.

.. ans: d, all of the above.

.. admonition:: Question

   In ``coding-events``, we add an additional private field, ``numberOfAttendees``, to the ``Event`` class. What other change must we make to ensure the user of our application can determine this value? (Assume we are using model binding to process form submission.) 

   #. Pass in a ``numberOfAttendees`` parameter to the form submission handler.
   #. Add another input element to the create event form with a ``name=numberOfAttendees`` attribute.
   #. Add a ``getAttendees`` method to ``EventData``.
   #. All of the above. 

.. ans: b, Add another input element to the create event form with a ``name=numberOfAttendees`` attribute.
