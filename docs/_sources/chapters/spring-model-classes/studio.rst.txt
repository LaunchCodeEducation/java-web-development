.. _user-signup-studio:

Studio: Spa User Signup
=======================

For this studio you will add functionality to allow users to sign up
for your ``spa-day`` app. 

The starter code has been modified from where you left off last class. Grab the refactored code 
on the `user-signup-starter branch <https://github.com/LaunchCodeEducation/spa-day-starter-code/tree/user-signup-starter>`__. 

You'll notice in this branch that the name field has been removed from the service selection form. Once we
implement user-signup functionality, we can use a given user's name to identify the spa client. We've also 
moved data into a ``Client`` model and out of the ``SpaDayController`` class.

In this studio, we'll ask you to write another model, ``User``. ``User`` and ``Client`` may at first 
appear redundant, but in the future as you develop your spa application, you may find a scenario where 
a user is logging in who is not also ``Client``.

Getting Ready
-------------

Within ``spa-day``, create the following files. 

#. Create a ``UserController`` in ``org.launchcode.spaday.controllers``. Add the
   ``@Controller`` annotation, along with ``@RequestMapping("user")`` to
   configure routes into the controller. 
#. Create a new folder, ``user/`` within ``resources/templates`` 
#. Create ``index.html`` and ``add.html`` templates within ``resources/templates/user/`` 
#. Create a ``User`` class within ``org.launchcode.spaday.models``

Creating the Model
------------------

Your ``User`` class should have a few private fields with getters and
setters: ``username``, ``email``, ``password``. 

Rendering the Add User Form
---------------------------

#. In the ``UserController``, create a handler method ``displayAddUserForm()`` to
   render the form. This handler should correspond to the path
   ``/user/add``, and for now, it can just return the path to the
   ``add.html`` template.

   .. admonition:: Tip

      Don't forget to add ``/user/add`` to your path when you test your new features. 

#. Within the ``add.html`` template, create a form that accepts inputs for
   each of the ``User`` class properties. Include an additional password input field to verify 
   the password input. The form should be set up to ``POST`` to ``/user``. 

#. Be sure to set ``type="password"`` for the password and verify inputs,
   to ensure the passwords are not visible when being typed into the form.
   You can also set ``type="email"`` on the email input, which will enable
   some basic client-side validation. We'll tackle validation in more detail 
   in the next studio. 

Processing Form Submission
--------------------------

#. Within the ``UserController``, create a handler method with this signature:

   .. sourcecode:: java

      public String processAddUserForm(Model model, @ModelAttribute User user, String verify) {
         // add form submission handling code here
      }

   This will use model binding to create a new user object, ``user``, and
   pass it into your handler method. 

   .. admonition :: Note
   
      You don’t need to store the ``User`` object anywhere for this studio.
      We’re focusing on form handling and validation in this exercise. If you
      want to keep track of users using the method we employed in the models
      lesson video, check out the Bonus Missions below.

#. Check that the ``verify`` parameter matches the
   password within the ``user`` object. If it does, render the
   ``user/index.html`` view template with a message that welcomes the user by 
   username. If the passwords don’t match, render the form again.

Refining Form Submission
------------------------

#. Once registered, we want the user to access the form selecting their spa services. 

   a. In ``user/index.html``, add a ``th:href`` element to take the user back to the root path, ``/``, of the app, where the ``serviceSelection`` template will be rendered.

#. If the form is re-rendered when a password is not verified, we should let the user know that their form
   was not properly submitted. Use ``model.addAttribute`` to add an ``error`` attribute, letting the user know 
   that their passwords should match. This model attribute will need to correspond to an element in the template that will only render the error text when the passwords do not match.

#. If we send a user back to re-populate the form, it would be nice to not clear their previous 
   submission. We won't need to save the password entries in this fashion.
   
   a. In the form submission handler, add the ``username`` and ``email`` fields of the submitted user as 
      model attributes. 
   
   #. Back in the form, add a value attribute to these form fields and make them equal to the
      model attributes. 

Bonus Missions
--------------

#. Add an ``id`` field to ``User``, along with accessor methods (with
   appropriate access level). Create a ``UserData`` class within
   ``org.launchcode.spaday.data`` that provides access to a list of users via
   ``add``, ``getAll``, and ``getById``.

   a. In the ``user/index.html`` view, display a list of
      all users by username. Each username should have a link that takes
      you to a detail page that lists the user’s username and email.

#. Add a ``Date`` field in ``User``, and initialize it to the time the
   user joined (i.e. when the ``User`` object was created). Display the
   value of this property in the user detail view.
