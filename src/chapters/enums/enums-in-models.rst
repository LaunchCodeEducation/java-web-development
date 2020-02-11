Enums in Model Classes
======================

One application of enum types is to represent categories of objects. We will take this approach in our ``coding-events`` application to categorize events based on their type, such as *conference* or *meetup*.

Enum Types in Models - Video
----------------------------

.. youtube::
   :video_id: FOvBYJxGPTQ
   :gh_path: LaunchCodeEducation/coding-events/enums

Enum Types in Models - Text
---------------------------

Create an Enum Class
^^^^^^^^^^^^^^^^^^^^

In your ``models`` package within ``coding-events``, create a new class called ``EventType``. 
Before you finish entering the name of your file, select the ``Enum`` option from the list of 
types.

.. figure:: figures/enumTypeSelection.png
   :scale: 50%
   :alt: Enum type selection.

Enum type selection.

Because enum values are constants, we use :ref:`naming-conventions` and write them in all caps.
Each value is demarcated with a comma and the list is completed with a semicolon.

``EventType``:

.. sourcecode:: java
   :lineno-start: 6

   public enum EventType {

      CONFERENCE,
      MEETUP,
      WORKSHOP,
      SOCIAL;

   }

Add an Enum Field
^^^^^^^^^^^^^^^^^

Enums can store additional information affiliated with each value in fields. Enum fields 
are treated like fields on any other type. Again, because enum values are constants, fields 
should be ``final`` variables, since they will not change. 

To add a ``displayName`` field to ``EventType``, we declare the field, add a constructor, and 
tack on a getter method:

.. sourcecode:: java
   :lineno-start: 13

   private final String displayName;

   EventType(String displayName) {
      this.displayName = displayName;
   }

   public String getDisplayName() {
      return displayName;
   }


To define the display name for each of the ``EventType`` values, we can call the constructor we 
just wrote like this:

.. sourcecode:: java
   :lineno-start: 6

   public enum EventType {

      CONFERENCE("Conference"),
      MEETUP("Meetup"),
      WORKSHOP("Workshop"),
      SOCIAL("Social");

      private final String displayName;

      EventType(String displayName) {
         this.displayName = displayName;
      }

      public String getDisplayName() {
         return displayName;
      }

   }

Add an Enum Property to a Model Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Other objects can have enum type properties. To add an ``EventType`` property to our model ``Event``,
we create a ``type`` field in ``Event`` amongst the other fields declared:

.. sourcecode:: java
   :lineno-start: 25

   // other Event field declarations

   private EventType type;

   // Event methods

We'll want to also add this field to the ``Event`` constructor, as well as a getter and setter 
method:

.. sourcecode:: java
   :lineno-start: 27

   private EventType type;

   public Event(String name, String description, String contactEmail, EventType type) {
      this();
      this.name = name;
      this.description = description;
      this.contactEmail = contactEmail;
      this.type = type;
   }

   public EventType getType() {
      return type;
   }

   public void setType(EventType type) {
      this.type = type;
   }

.. _passing-enums-through-controller:

Pass Enum Values Through the Controller
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``coding-events`` uses model binding to create an ``Event`` object. So like any other field on 
the model, the controller does not necessarily need to know about the addition of ``Event.type`` 
in order to create an ``Event`` instance from a form. However, we want the user to choose from 
the pre-defined event type values when creating their event. To do this, we'll use the 
controller method ``displayCreateEventForm`` to pass those values into the view.

In ``EventController``:

.. sourcecode:: java
   :lineno-start: 26

   @GetMapping("create")
   public String displayCreateEventForm(Model model) {
      model.addAttribute("title", "Create Event");
      model.addAttribute(new Event());
      model.addAttribute("types", EventType.values());
      return "events/create";
   }

``.values()`` is a built-in static method that returns an array of values defined in 
the given enum, in the order in which they have been declared.

With the template variable ``types`` now defined, we can use our ``EventType`` values in the view.

Use Enum Value in a ``Select`` Element
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The list of constants returned from ``EventType`` lends itself well to a ``select``-type form 
input. We'll update our form so that a user will have the option to choose one of the provided 
event types from a dropdown menu.

In ``templates/events/create.html``:

.. sourcecode:: html
   :lineno-start: 27

   <div class="form-group">
      <label> Type
      <select th:field="${event.type}">
         <option th:each="type : ${types}"
                  th:value="${type}"
                  th:text="${type.displayName}"
         ></option>
      </select>
      </label>
   </div>

As with the other form inputs on the page, the ``th:field`` attribute determines the ``name``
and ``id`` attributes for the ``select`` tag. We make an ``option`` tag for each of the ``EventType``
values, making use of the ``types`` variable we passed in from the controller in 
:ref:`the previous step <passing-enums-through-controller>`. We set the ``value`` attribute for the 
model data to be the ``EventType`` value using ``th:value``. And the type name shown to the user 
of the form as the ``displayName`` of the type, using ``th:text``.

Use Enum Properties to Display Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once an event is created, to display its ``type`` field in the table of all events, we'll modify 
``templates/events/index.html`` to include another column:

::

   <!-- other table headers -->
   <th>Type</th>
   <!-- other event data -->
   <td th:text="${event.type.displayName}"</td>

In this case, the type displayed is the value of the event object's ``type`` field, so the controller 
method responsible for rendering this view does not need a ``types`` variable passed in. To show the 
more user-friendly view of the type value, we use the ``.displayName`` field of ``EventType``.

Check Your Understanding
------------------------

.. admonition:: Question

   When we add a field to the ``EventType`` enum from ``coding-events``, what is the strongest 
   reason why we don't we write a setter method for that field?

   #. Enum classes cannot contain setter methods
   #. Final variables cannot be reassigned
   #. Enum fields cannot be reassigned
   #. We don't use a setter method in the rest of the application

.. ans: b, Final variables cannot be reassigned

.. admonition:: Question

   In ``coding-events``, say we change our template variable name in 
   ``EventController.displayCreateEventForm`` so that ``EventType.values()`` is now assigned to 
   a variable, ``categories``. Which of the template expressions in the following codeblock 
   from ``create.html``, if any, should be changed to reflect this update? Select all that apply.

   .. sourcecode:: html
      :lineno-start: 27

      <div class="form-group">
         <label> Type
         <select th:field="${event.type}">
            <option th:each="type : ${types}"
                     th:value="${type}"
                     th:text="${type.displayName}"
            ></option>
         </select>
         </label>
      </div>

   #. In line 29, ``${event.type}`` should be changed to ``${event.category}``
   #. In line 30, ``type : ${types}`` should be changed to ``category : ${categories}``
   #. In line 31, ``${type}`` should be changed to ``${category}``
   #. In line 32, ``${type.displayName}`` should be changed to ``${category.displayName}``

.. ans: b, c, and d, lines 30,31, and 32
