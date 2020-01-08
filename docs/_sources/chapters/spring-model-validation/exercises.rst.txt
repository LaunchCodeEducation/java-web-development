Exercises: Model Validation
===========================

Let’s practice adding more fields onto our event objects and 
validating them. Create a new branch from the `display-errors branch <https://github.com/LaunchCodeEducation/coding-events/tree/display-errors>`__. 

Below, we describe some new fields for you to add to the ``Event`` class. 
For each field, consider the following factors:

a. What will you call your field?
#. Will you need accessors for this field?
#. What type of input should be added to capture the field's information from the user?
#. Refer to the documentation page to find an appropriate annotation to fit the constraints. 
#. What should the error message convey to the user?
#. What, if anything, will you need to update on the controller to account for the new field?

Event information to add:

#. Add a field to collect information about where the event will take place. This field should not be 
   null or blank. 

#. Add a field to collect information about whether an attendee must register for the event or not. For 
   the purposes of validation practice, make this field only able to be marked as true. 

#. Add a field to collect information about the number of attendees for the event. Valid values for this 
   field should be any number over zero.

#. Browse the validation annotations to find one to use on another new field of your choosing.


