.. _model-validation-exercise-solutions:

Exercise Solutions: Model Validation
====================================

Event information to add:

.. _model-validation-exercise-solutions1:

#. Add a field to collect information about where the event will take place. This field should not be 
   null or blank. 

   .. sourcecode:: java

      @NotBlank(message="Location cannot be left blank.")
      private String location;

   :ref:`Back to the exercises <model-validation-exercises>`

.. _model-validation-exercise-solutions3:

3. Add a field to collect information about the number of attendees for the event. Valid values for this 
   field should be any number over zero.

   .. sourcecode:: java
   
      @Positive(message="Number of attendees must be one or more.")
      private int numberOfAttendees;

   :ref:`Back to the exercises <model-validation-exercises>`

