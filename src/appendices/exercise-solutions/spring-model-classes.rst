.. _model-classes-exercise-solutions:

Exercise Solutions: Edit Model Classes
======================================

#. Create the two handler methods listed below in ``EventController``. We’ll add code
   to these in a moment, so just put the method outline in place for
   now.

   .. sourcecode:: java

      @Controller
      @RequestMapping("events")
      public class EventController {
      
         @GetMapping
         public String displayAllEvents(Model model) {
            model.addAttribute("title", "All Events");
            model.addAttribute("events", EventData.getAll());
            return "events/index";
         }
      
         @GetMapping("create")
         public String displayCreateEventForm(Model model) {
            model.addAttribute("title", "Create Event");
            return "events/create";
         }
      
         @PostMapping("create")
         public String processCreateEventForm(@ModelAttribute Event newEvent) {
            EventData.add(newEvent);
            return "redirect:";
         }
      
         @GetMapping("delete")
         public String displayDeleteEventForm(Model model) {
            model.addAttribute("title", "Delete Events");
            model.addAttribute("events", EventData.getAll());
            return "events/delete";
         }
      
         @PostMapping("delete")
         public String processDeleteEventsForm(@RequestParam(required = false) int[] eventIds) {
      
            if (eventIds != null) {
                  for (int id : eventIds) {
                     EventData.remove(id);
                  }
            }
      
            return "redirect:";
         }
      
         @GetMapping("edit/{eventId}")
         public String displayEditForm(Model model, @PathVariable int eventId){
         }
      
         @PostMapping("edit")
         public String processEditForm(int eventId, String name, String description) {
         }
      
      }
   
#. Create an ``edit.html`` view template in ``resources/templates/events``.
#. Back in the ``displayEditForm`` handler, round out the controller method.

   .. sourcecode:: java

      @GetMapping("edit/{eventId}")
      public String displayEditForm(Model model, @PathVariable int eventId){
         Event eventToEdit = EventData.getById(eventId);
         model.addAttribute("event", eventToEdit);
         String title = "Edit Event " + eventToEdit.getName() + " (id=" + eventToEdit.getId() + ")";
         model.addAttribute("title", title );
         return "events/edit";
      }
#. Add another input to hold the id of the event being edited. This
should be hidden from the user:

   .. sourcecode:: html

      <input type="hidden" th:value="${event.id}" name="eventId" />   
#. In ``processEditForm``, 
   
   .. sourcecode:: java

      @PostMapping("edit")
      public String processEditForm(int eventId, String name, String description) {
         Event eventToEdit = EventData.getById(eventId);
         eventToEdit.setName(name);
         eventToEdit.setDescription(description);
         return "redirect:";
      }

