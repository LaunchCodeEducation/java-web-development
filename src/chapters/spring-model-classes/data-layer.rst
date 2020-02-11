.. _data-layer:

Models and Data 
===============

In order to work with data, we need to add another element to our MVC application. Say for example,
we want to do things like remove an event from our list. Well, if two events both have the same name, 
how might we identify which of those items to delete? We can't yet. So we need to tweak how we store
event data. 

In ``coding-events``, we add a unique identifier field to ``Events`` to better handle and track distinct 
``Event`` instances. We'll also create another model class called ``EventData`` to encapsulate data storage 
and prepare ourselves for decoupling data from controller classes.

Add a Unique Id - Video
-----------------------

.. youtube::
   :video_id: ijnIgreiNHU
   :gh_path: LaunchCodeEducation/coding-events/add-id

.. index:: ! uid

Add a Unique Id - Text
-----------------------

Identifying data by a user-defined string called ``name`` is not a sustainable or scalable method
of handling data in most situations. Consider the address book example. How can
we distinguish between two contact entries with the same name field? It is a frequent
practice to add a **unique identifier** field (sometimes called, or even labelled, **uid**) to a class 
responsible for modelling data. This ensures that our address book can contain two separate entries for 
our contacts who have the same name as one another. 

To accomplish the same data clarity with events, we'll add a few things to the event model class:

#. A private ``id`` field .
#. A static counter variable, ``nextId``.
#. Additional constructor code that:
   
   a. Sets the ``id`` field to the ``nextId`` value.
   b. Increments ``nextId``.

#. A getter method for the ``id`` field.

The result in ``models/Event,java``:

.. sourcecode:: java
   :lineno-start: 6

   public class Event {

      private int id;
      private static int nextId = 1;

      private String name;
      private String description;

      public Event(String name, String description) {
         this.name = name;
         this.description = description;
         this.id = nextId;
         nextId++;
      }

      public int getId() {
         return id;
      }

      // ... other getters and setters ... //

   }

With these additions, every time a new event object is created it is assigned a unique integer to its ``id`` field.

Create a Data Layer - Video
---------------------------

.. youtube::
   :video_id: 8AQtYZ_q57M
   :gh_path: LaunchCodeEducation/coding-events/create-data-layer

Create a Data Layer - Text
--------------------------

Now that we've begun building a model, it's a good time to remind ourselves that models are not designed to be 
data storage containers. Rather, models are meant to shape the data stored in another location into objects that 
can be used in our application. As we work our way into learning about database usage and service calls, however, 
we'll use a Java class to store some data temporarily. 

Create a new package called ``data`` and add a class ``EventData``. Whereas ``Event`` is responsible for organizing
user-inputted information into a Java object, ``EventData`` is responsible for maintaining those objects once they 
are created. ``EventData`` is itself a Java class that stores events. It contains several methods for managing and 
maintaining the event data that simply extend built-in HashMap methods.

The contents of ``data/EventData.java``:

.. sourcecode:: java
   :lineno-start: 12

   public class EventData {

      private static Map<Integer, Event> events = new HashMap<>();

      public static Collection<Event> getAll() {
         return events.values();
      }

      public static void add(Event event) {
         events.put(event.getId(), event);
      }

      public static Event getById(Integer id) {
         return events.get(id);
      }

      public static void remove(Integer id) {
         if (events.containsKey(id)) {
            events.remove(id);
         }
      }

   }


With ``EventData`` managing event data, we must once again refactor ``EventController`` to update the items stored in 
``EventData``. In keeping with the objective to remove data handling from the controller, we'll remove the list 
of events at the top of the class. Consequently, for the ``displayAllEvents`` handler, we'll now use events from 
``EventData`` in ``addAttribute()``:

.. sourcecode:: java
   :lineno-start: 25

   model.addAttribute("events", EventData.getAll());

And back to ``processCreateEventForm``, we'll make use of the ``.add()`` method from ``EventData``:

.. sourcecode:: java
   :lineno-start: 37

   EventData.add(new Event(eventName, eventDescription));


Delete an Event - Video
-----------------------

.. youtube::
   :video_id: orsBBbDaJMM
   :gh_path: LaunchCodeEducation/coding-events/delete-events

Delete an Event - Text
----------------------

Now that we've refined our events storage method, we are able to tackle the task of deleting an object. 
To delete an event object from storage, we'll grab the event's id and use that
information to call the ``remove`` method of ``EventData``.
Since the delete event is user-initiated, a controller will be involved to pass
the information from the user-accessible view to the data layer. So our first step
with this task is to create a controller method to get a view to delete events.

Onto the end of ``EventController``, add the following method:

.. sourcecode:: java
   :lineno-start: 41

   @GetMapping("delete")
   public String renderDeleteEventForm(Model model) {
      model.addAttribute("title", "Delete Event");
      model.addAttribute("events", EventData.getAll());
      return "events/delete";
   }

We'll now need to create a new view for the path mapped in the method above. Add a new template, 
``events/delete.html``. This view will reference event id fields in order to distinguish which items the user 
will request to delete via checkbox inputs. 

.. sourcecode:: html
   :linenos:

   <!DOCTYPE html>
   <html lang="en" xmlns:th="http://www.thymeleaf.org/">
      <head th:replace="fragments :: head"></head>
      <body class="container">

         <header th:replace="fragments :: header"></header>

         <form method="post">

            <th:block th:each="event : ${events}">
               <div class="form-group">
               <label>
                     <span th:text="${event.name}"></span>
                     <input type="checkbox" name="eventIds" th:value="${event.id}" class="form-control">
               </label>
               </div>
            </th:block>

            <input type="submit" value="Delete Selected Events" class="btn btn-danger">
         </form>

      </body>
   </html>

We also need a ``POST`` handler to take care of what to do when the delete event information
is submitted by the user. We'll have this post handler redirect the user back to the home 
page once they have selected which event, or events, to remove from storage.

In ``EventController``, add another controller method:

.. sourcecode:: java
   :lineno-start: 50

   @PostMapping("delete")
   public String processDeleteEventsForm(@RequestParam(required = false) int[] eventIds) {

        if (eventIds != null) {
            for (int id : eventIds) {
                EventData.remove(id);
            }
        }

        return "redirect:";
   }

This handler method uses the ``required = false`` parameter of ``@RequestParam`` to make this parameter optional. This allows the user to submit the form without any events selected. Once ``eventIds`` is optional, we must also check that it is not ``null`` before entering the loop. 

Check Your Understanding
-------------------------

.. admonition:: Question

   In ``coding-events``, which method can we call to list every event object?

   #. ``Events.get()`` 
   #. ``EventData.getEvery()`` 
   #. ``Event.getAll()`` 
   #. ``EventData.getAll()`` 

.. ans: d, ``EventData.getAll()``

.. admonition:: Question

   In ``coding-events``, breaking up the event storage from the ``Event`` model is an example of which object-oriented
   concept?

   #. Inheritance
   #. Polymorphism
   #. Encapsulation 
   #. MVC design

.. ans: c, encapsulation
