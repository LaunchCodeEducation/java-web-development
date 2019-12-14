Exercises: Model Validation
===========================

Let’s practice adding more fields onto our event objects and 
validating them. Create a new branch from TODO: STARTING CODE BRANCH. For each of the items below,
consider the following factors:

a. What will you call your field?
#. Will you need accessors for this field?
#. What type of input should be added to capture the field's information from the user?
#. Refer to the documentation page to find an appropriate annotation to fit the constraints. 
#. What should the error message convey to the user?
#. What, if anything, will you need to update on the controller to account for the new field?

Event information to add:

#. Add a field to collect information about where the event will take place. This field should not be 
   null or blank. Things to consider:

#. Add a field to collect information about whether an attendee must register for the event or not. For 
   the purposes of validation practice, make this field only able to be marked as true. 

#. Add a field to collect information about the number of attendees for the event. Valid values for this 
   field should be any number over zero.

#. Browse the validation annotations to find one to use on another new field of your choosing.


.. validation to our ``edit`` handlers. Make sure your ``coding-events`` app 
..    resembles the `end-of-validation-errors <TODO>`__.

..    In the ``edit`` handler that displays the form, you should already be
..    passing in the ``Event`` object to be edited. This means that we can
..    refactor the form in the ``edit.html`` template to use
..    ``th:object="${event}"`` and then use ``th:field="*{propertyName}"``
..    to help render the inputs. Don’t forget to modify the ``<label>``
..    elements to use ``th:for="propertyName"``. Add error message elements
..    for each of the properties.

..    .. TODO: remove this?

..    You’ll also want to pass in the list of all ``EventType`` enum
..    values, as we did in the ``add.html`` form from the `lesson
..    video <./../videos/intro-to-spring-boot-enums/>`__. You’ll want to
..    pre-select the specific option that is already stored on the given
..    object.

..    In the ``edit`` handler that processes the form, validate the model
..    and respond appropriately.

.. 2. Add an integer property to ``Event`` to allow the user to give each
..    event a rating. Follow these steps:

..    -  Add the property to ``Event.java``, along with `validation
..       annotations <http://docs.oracle.com/javaee/6/tutorial/doc/gircz.html>`__
..       to allow the user to enter a value between 1 and 5
..    -  Add the form input, label, and error message display to
..       ``templates/event/add.html``
..    -  Display the rating in ``templates/events/index.html``
..    -  Add the rating to the ``edit.html`` template
..    -  Test!
