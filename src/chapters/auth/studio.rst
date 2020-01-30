Studio: TechJobs Authentication
===============================

For this studio, you'll be tasked with adding simple user authentication to your 
``techjobs`` application. The steps to do this will match what you have already done 
in ``coding-events``. You should refer back to the tutorial starting 
:ref:`here <user_auth_walkthrough>`.

#. :ref:`auth_studio_user_model`
#. :ref:`auth_studio_forms`
#. :ref:`auth_studio_filter`


.. _auth_studio_user_model:

Create the User Model
---------------------

#. Create a ``User`` model identical to that in ``coding-events``. The class needs:

   #. To be an entity.
   #. To have username and encrypted password fields.
   #. To have appropriate constructors, getters, setters.

#. Encode the ``User`` password field.

   #. Add a static ``BCryptPasswordEncoder`` variable.
   #. Update the constructor that has arguments to encode the password field.
   #. Add a method to check password values.

#. Create a ``UserRepository``.

   #. Add the special query method to find a user by username.
   

.. _auth_studio_forms:

Create the Login and Registration Forms
---------------------------------------

#. Create an ``AuthenticationController``.

   #. Include an autowired ``UserRepository``.

#. Add session handling utilities. This includes:

   #. A static final variable for the session key.
   #. A method to get the user information from the session.
   #. A method to set the user in the session.

#. Create two DTOs for the user registration and login forms.

   #. Create a login form DTO with username and password fields.
   #. Create a register form DTO with the fields above and a field to verify a password.

#. Handle the registration data.

   #. Add a ``GET`` handler in ``AuthenticationController`` to display a registration form.
   #. Create a register template with form fields corresponding to the register DTO.
   #. Create a ``POST`` handler in ``AuthenticationController`` to process the form.

      #. If the form has validation errors, re-render the registration form with a useful message.
      #. If the username is already tied to a user, add a fitting error message and re-render the form.
      #. If the two form fields for passwords do not match, add an error message and re-render the form.
      #. If none of the above conditions are met, 
      
         #. Create a new user with the form data, 
         #. Save the user to the database, 
         #. Create a new user session,
         #. Redirect to the home page.

#. Handle the login data.

   #. Repeat steps 1 + 2 for handling the registration data, this time with the login information.
   #. Apart from model validation checks and the final redirect, the ``POST`` handler for the login form will 
      have some different checks from that of the registration form:

      #. If the database does not contain a user with the submitted username, add an error message and re-render.
      #. If the submitted password does not match the encoded password attached to the username in the form, 
         add an error message and re-render.
      #. If the submission passes all of these checks, create a new user session.

#. Handle logging out.

   #. Still in ``AuthenticationController``, create a ``GET`` handler method for a path to logout.

      #. Invalidate the session data from the request object.
      #. redirect the user to the login form.

.. _auth_studio_filter:

Filter Requests
---------------
19.5.1. Request Filters in Spring
19.5.2. Creating AuthenticationFilter
19.5.2.1. Overriding preHandle
19.5.2.2. Creating a Whitelist
19.5.3. Registering the Filter With Spring
