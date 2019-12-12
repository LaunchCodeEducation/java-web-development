Exercises: Edit Model Classes
=============================

Add functionality to edit event objects in the ``coding-events`` application. 
These exercises assume that you have added all of the code from this section of the book and your 
application resembles the `model-binding branch <https://github.com/LaunchCodeEducation/coding-events/tree/model-binding>`__.

The edit form will resemble the form used to create an event.

.. admonition:: Tip 

   As you work through these steps, test your code along the way! 
   With each change you apply to your code, ask yourself what you expect to see when the application
   is run. You may not find that all of the steps result in observable changes, though.
   Use IntelliJ’s debugger and read your error messages if you run into issues after applying any of
   the changes.

#. Create the two handler methods listed below in ``EventController``. We’ll add code
   to these in a moment, so just put the method outline in place for
   now.

   #. Create a method to display an edit form with this signature:

      .. sourcecode:: java
         :linenos:

         public String displayEditForm(Model model, @PathVariable int eventId) {
            // controller code will go here
         }

   #. Create a method to process the form with this signature:

      .. sourcecode:: java
         :linenos:

         public String processEditForm(int eventId, String name, String description) {
            // controller code will go here
         }

#. Add the necessary annotations to these methods for them to both live
   at the path ``/events/edit``.
    
   #. Judging by the names of the handlers, which should handle ``GET`` requests and which should 
      handle ``POST`` requests?
   
   #. Remember, we’ve configured ``@RequestMapping`` with a URL segment on the controller class already.

   #. You’ll need to configure the route for ``displayEditForm`` to include the path variable ``eventId``, 
      so that paths like ``/events/edit/3`` will work.

#. Create an ``edit.html`` view template in
   ``resources/templates/events``.

#. Copy the code from ``create.html`` into ``edit.html``. 

   #. You'll want to update the text of the submit button to reflect the edit functionality.

#. Back in the ``displayEditForm`` handler, round out the controller method.

   #. Use an ``EventData`` method to find the event object with the given ``eventId``.
   
   #. Put the event object in the ``model`` with ``.addAttribute()``.

   #. Return the appropriate template string.

#. Within the form fields in ``edit.html``, 

   #. Get the name and description from the event that was passed in via the ``model`` and
      set them as the values of the form fields.
   
   #. Add ``th:action="@{/events/edit}"`` to the ``form`` tag.

#. Add another input to hold the id of the event being edited. This
   should be hidden from the user:

   .. sourcecode:: html

      <input type="hidden" th:value="${event.id}" name="eventId" />

#. Back in the ``displayEditForm`` handler, add a title to ``model`` that reads “Edit Event
   NAME (id=ID)” where NAME and ID are replaced by the values for the
   given event. 

#. In ``processEditForm``, 

   #. Query ``EventData`` for the event being edited with the given id parameter. 
   
   #. Update the name and description of the event with the appropriate model setter methods.

   #. Redirect the user to ``/events`` (the event listing page).

#. To access event editing, the user will need an edit option in the list of event data.

   #. In ``resources/templates/events/index.html``, add a link in a new table column to edit the 
      event:

      .. sourcecode:: html
         :linenos:

         <td>
            <a th:href="@{/events/edit/{id}(id=${event.id})}">Edit</a>
         </td>

