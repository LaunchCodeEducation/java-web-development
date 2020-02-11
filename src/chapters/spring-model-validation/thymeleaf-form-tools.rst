Thymeleaf Form Tools
====================

Thymeleaf provides some handy attributes for working with form fields. They make use of the fact that, when using model binding, each model field contains a lot of information about the corresponding form input needed. In particular, the model field and its annotations often determine:

#. The name of the form field (that is, the value of its ``name`` attribute).
#. The validation rules and corresponding error messages for the field.

Thymeleaf provides some convenient attributes to make wiring up a form much easier and cleaner.

Display Validation Errors for a Field - Video
----------------------------------------------

.. youtube::
   :video_id: yc-bSDSDuKg
   :gh_path: LaunchCodeEducation/coding-events/display-errors

Display Validation Errors for a Field - Text
--------------------------------------------

Using ``th:field``
^^^^^^^^^^^^^^^^^^

.. index:: ! th:field

We can use the ``th:field`` attribute on a form input to instruct Thymeleaf to add field-specific attributes to the form, such as ``name`` and ``id``. 

Consider our second input, which currently looks like this:

.. sourcecode:: html
   :lineno-start: 17

   <label>Description
      <input type="text" name="description" class="form-control">
   </label>

Above, we set the ``name`` attribute of the input element equal to ``description"``. We do this because we want this input data to be bound to the ``description`` field of the ``Event`` class when the form is submitted.

A better approach uses ``th:field`` to bind the ``description`` field *when the form is rendered*.

.. sourcecode:: html
   :lineno-start: 17

   <label>Description
      <input type="text" th:field="${event.description}" class="form-control">
   </label>

With this syntax, Thymeleaf will look for a variable named ``event`` and use its ``description`` property to set the values of the ``name`` and ``id`` attributes. The generated input looks like this:

.. sourcecode:: html

   <input type="text" id="description" name="description" class="form-control">

We don't need to use the ``id`` attribute in this case, but it doesn't hurt anything by being there. Now, Thymeleaf sets ``name`` on its own, based on the field identifier. 

.. index:: no-arg constructor

For this to work, two more steps are necessary. First, we add constructor to ``Event`` that doesn't require any arguments, also called a **no-arg constructor**.

.. sourcecode:: java
   :lineno-start: 27

   public Event(String name, String description, String contactEmail) {
      this();
      this.name = name;
      this.description = description;
      this.contactEmail = contactEmail;
   }

   public Event() {
      this.id = nextId;
      nextId++;
   }

This code includes two changes:

#. A no-arg constructor has been created. It simply sets the ``id`` of the object, leaving all other fields ``null``.
#. The previously-existing constructor now calls ``this()``, which calls the no-arg constructor to set the ``id`` before setting the values of all other fields. 

Finally, we have to pass in an empty ``Event`` created with the new no-arg constructor when rendering the form. Back in ``EventController``, we update the handler:

.. sourcecode:: java
   :lineno-start: 26

   @GetMapping("create")
   public String displayCreateEventForm(Model model) {
      model.addAttribute("title", "Create Event");
      model.addAttribute("event", new Event());
      return "events/create";
   }

Notice line 29, which passes in an ``Event`` object created by calling the no-arg constructor. 

.. admonition:: Note

   It's also allowable to pass in the ``Event`` object without a label:

   .. sourcecode:: java

      model.addAttribute(new Event());

   In this case, Spring will implicitly create the label ``"event"``, which is the lowercase version of the class name. 

Using this technique on our other form fields completes the task of binding the object to the form during rendering.

.. sourcecode:: html
   :lineno-start: 8

   <form method="post">
      <div class="form-group">
         <label>Name
               <input type="text" th:field="${event.name}" class="form-control">
         </label>
         <p class="error" th:errors="${event.name}"></p>
      </div>
      <div class="form-group">
         <label>Description
               <input type="text" th:field="${event.description}" class="form-control">
         </label>
         <p class="error" th:errors="${event.description}"></p>
      </div>
      <div class="form-group">
         <label>Contact Email
               <input type="text" th:field="${event.contactEmail}" class="form-control">
         </label>
         <p class="error" th:errors="${event.contactEmail}"></p>
      </div>
      <div class="form-group">
         <input type="submit" value="Create" class="btn btn-success">
      </div>
   </form>

One additional result of using ``th:field`` is that if the ``Event`` object has a value in any bound field, the input will be created with that value in its ``value`` attribute. For example, if the ``event`` object has a ``contactEmail`` of ``me@me.com``, then the resulting form input would be:

.. sourcecode:: html

   <input type="text" id="contactEmail" name="contactEmail" value="me@me.com" class="form-control">

The value is then visible in the form field when the page loads. This may not seem immediately useful, but it actually is. Recall our form submission handler:

.. sourcecode:: java
   :lineno-start: 33

   @PostMapping("create")
   public String processCreateEventForm(@ModelAttribute @Valid Event newEvent,
                                       Errors errors, Model model) {
      if(errors.hasErrors()) {
         model.addAttribute("title", "Create Event");
         return "events/create";
      }

      EventData.add(newEvent);
      return "redirect:";
   }

This method checks for validation errors and returns the user to the form if it finds any. It uses model binding to create a new event object, but this event object is *also passed into the view when re-rendering the form*. This means that if there are validation errors, the form will be rendered with the values that the user previously entered, preventing the user from having to re-enter all of their data.

Using ``th:errors``
^^^^^^^^^^^^^^^^^^^

The Thymeleaf attribute ``th:errors`` is used similarly to ``th:field`` to display field-specific error messages. Recall that when we added our validation annotations to each model field, we also :ref:`added a message argument <validation-messages>`. Setting ``th:errors`` to a field will display any validation errors for that field.

For example, let's add a new element to the first form group:

.. sourcecode:: html
   :lineno-start: 9

   <div class="form-group">
      <label>Name
         <input th:field="${event.name}" class="form-control">
      </label>
      <p class="error" th:errors="${event.name}"></p>
   </div>

Setting ``th:errors="${event.name}"`` tells Thymeleaf to insert any error messages related to the ``name`` field of ``event`` into the paragraph element. We add ``class="error"`` to allow us to style this element, for example with red text. A simple rule in our ``styles.css`` file will do the trick:

.. sourcecode:: css

   .error {
     color: red;
   }

.. admonition:: Note

   Make sure that ``styles.css`` is included in the ``head`` fragment of ``fragments.html``, or the stylesheet will not load.

Using this attribute on all of the fields gives us our final form template code:

.. sourcecode:: html
   :lineno-start: 8

   <form method="post">
      <div class="form-group">
         <label>Name
               <input type="text" th:field="${event.name}" class="form-control">
         </label>
         <p class="error" th:errors="${event.name}"></p>
      </div>
      <div class="form-group">
         <label>Description
               <input type="text" th:field="${event.description}" class="form-control">
         </label>
         <p class="error" th:errors="${event.description}"></p>
      </div>
      <div class="form-group">
         <label>Contact Email
               <input type="text" th:field="${event.contactEmail}" class="form-control">
         </label>
         <p class="error" th:errors="${event.contactEmail}"></p>
      </div>
      <div class="form-group">
         <input type="submit" value="Create" class="btn btn-success">
      </div>
   </form>

Now, when the form is submitted with invalid data, our custom validation error messages will display just below the given inputs.

.. figure:: figures/display-validation-errors.png
   :alt: Our Create Event form after submission with all fields blank. Red error messages are visible next to the fields that failed validation.
   :width: 700px

   The result of submitting an empty form

Check Your Understanding
------------------------

.. admonition:: Question

   Which HTML attributes will a ``th:field`` attribute NOT influence?

   #. ``id``
   #. ``name``
   #. ``value``
   #. ``field``

.. ans: D, which is not even an attribute. All other attributes are set by th:field
