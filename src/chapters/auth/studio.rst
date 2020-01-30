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

#. Create an ``AuthenticationFilter`` class in the top level of the app.

   #. Have this class inherit from ``HandlerInterceptorAdapter``.
   #. Add autowired instances of both ``UserRepository`` and ``AuthenticationController``.
   #. Add a ``preHandle`` method.

      #. This must override the inherited method of the same name.
      #. Grab the session information from the request object.
      #. Query the the session data for a user.
      #. If a user exists, return true. Otherwise, redirect to the login page and return false.

#. Create a whitelist.

   #. In the top of ``AuthenticationFilter``, add a whitelist variable containing the paths that can be 
      accessed without a user session.
   #. Create a method next that checks a given path against the values in the whitelist. 
   #. Update ``preHandle`` with a call to this method.

      #. Before looking for session and user status, add a conditional that checks the whitelist status 
         of the current request object.

#. Register the filter with Spring

   #. Create a class called ``WebApplicationConfig``
