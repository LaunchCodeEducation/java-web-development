Models and Data 
===============

In order to work with data, we need to add another element to our MVC application. Say for example,
we want to do things like remove an event from our list. Well, if two events both have the same name, 
how might we identify which of those items to delete? We can't yet. So we need to tweak how we store
event data. 

In ``coding-events``, we add a unique identifier field to ``Events`` to better handle distinct ``Event`` 
instances. We'll also create another model class called ``EventData`` to encapsulate data storage and prepare
ourselves for decoupling data from model classes.

Add a Unique Id - Video
-----------------------

.. todo:: video adding a unique id generator

.. index:: ! uid

Add a Unique Id - Text
-----------------------

Identifying data by a string ``name`` is not a sustainable or scalable method
of handling data in most situations. Consider the address book example. How can
we distinguish between two contact entries with the same name field? It is a frequent
practice to add a **unique identifier** field (sometimes called, or even labelled, **uid**) to a class 
responsible for modelling data. This ensures that our address book can contain two separate entries for 
our contacts who have the same name as one another. 

To accomplish the same data clarity with events, we'll add a few things to the event model class:

#. A private ``id`` field .
#. A static counter variable, ``nextId``.
#. A no-arg constructor that:
   
   a. Sets the ``id`` field to the ``nextId`` value.
   b. Increments ``nextId``.

#. A call to the default constructor in all other constructors.
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
         this();
         this.name = name;
         this.description = description;
      }

      private Event() {
         this.id = nextId;
         nextId++;
      }

      public int getId() {
         return id;
      }

      // ... other getters and setters ... //

   }

With these additions, every time a new event object is created, the default constructor is used, therefore 
lending all event instances with their own unique identifier property, ``id``.

Create a Data Layer - Video
---------------------------

.. todo:: video showing creation of EventData class

Create a Data Layer - Text
--------------------------

Now that we've begun building a model, it's a good time to remind ourselves that models are not designed to be 
data storage containers. Rather, models are meant to shape the data stored in another location into objects that 
can be used in our application. As we work our way into learning about database usage and service calls, however, 
we'll use a model to store some data temporarily. 

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

.. todo:: video showing event deletion

Delete an Event - Text
----------------------

Now that we've refined our events storage method, we are able to tackle the task of deleting an object. 
To delete an event object from storage, we'll grab the event's id and use that
information to call the ``remove`` method.
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
            <div th:each="event : ${events}" class="form-group">
               <label>
                  <input type="checkbox" th:value="${event.id}" name="eventIds" class="form-control">
                  <span th:text="${event.name}"></span>
               </label>
            </div>

            <input type="submit" value="Delete Selected Events" class="btn btn-danger">
         </form>

      </body>
   </html>

We also need a ``POST`` handler to take care of what to do when the delete event information
is submitted by the user. We'll have this post handler redirect the user back to the home 
page once they have selected which event, or events, to remove from storage.

In ``EventController``, add another controller method:

.. sourcecode:: java
   :lineno-start: 48

   @PostMapping("delete")
   public String processDeleteEventForm(@RequestParam int[] eventIds) {

      for (int eventId : eventIds) {
         EventData.remove(eventId);
      }

      return "redirect:";
   }


Check Your Understanding
-------------------------

.. admonition:: Question

   Which method can we call to list every event object?

   #. ``Events.get()`` 
   #. ``EventData.getEvery()`` 
   #. ``Event.getAll()`` 
   #. ``EventData.getAll()`` 

.. ans: d, ``EventData.getAll()``
