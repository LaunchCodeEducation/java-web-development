Studio: TechJobs Authentication
===============================

For this studio, you'll be tasked with adding simple user authentication to your 
``techjobs`` application. The steps to do this will match what you have already done 
in ``coding-events``. You should refer back to the tutorial starting 
:ref:`here <user_auth_walkthrough>`.

#. :ref:`auth_studio_user_model`
#. :ref:`auth_studio_forms`
#. :ref:`auth_studio_filter`

The Starter Code
----------------

#. Fork and clone the starter code for 
   `TechJobs (Auth Edition) <https://github.com/LaunchCodeEducation/java-web-dev-techjobs-authentication>`__.

#. The dependencies for the database connection and hashing function 
   are already added for you in ``build.gradle``. You will need to 
   do some work to ensure that the schema, user, and database password 
   match your own local MySQL setup.

   #. Open ``application.properties`` and view the first three statements:

      ::  

         # Database connection settings
         spring.datasource.url=jdbc:mysql://localhost:3306/techjobs_auth
         spring.datasource.username=techjobs_auth
         spring.datasource.password=auth

   #. You likely do not already have a schema named ``techjobs_auth`` or 
      this combination of username and password so you must create them.

      .. admonition:: Tip
      
         To create a new schema in your current connection, refer 
         back to the instructions in :ref:`sql-part1-exercises`.

         To create a new user with permissions, refresh your memory
         in :ref:`setup-orm-database`.

.. admonition:: Note
   
      We've greatly reduced the functionality of the app so you can focus
      on the work to set up authentication. Running the application now 
      gives you a familiar-looking navbar with two menu options, *Add Jobs* and *Logout*.
      You can add jobs right away and an astute observer of the starter code and
      schema tables will notice that the fields on ``Job`` are only strings, not
      complex objects. Logout functionality is not yet implemented, but you'll get there by the end of 
      this studio.

.. _auth_studio_user_model:

Create the User Model
---------------------

#. In the project you have cloned, create a ``User`` model identical to that in ``coding-events``. The class needs:

   #. To be an entity.
   #. To have username and encrypted password fields.
   #. To have appropriate constructors, getters, setters.

#. Encode the ``User`` password field.

   #. Add a static ``BCryptPasswordEncoder`` variable.
   #. Update the constructor that has arguments to encode the password field.
   #. Add a method to check password values.

#. Create a ``UserRepository``.

   #. Add the special query method to find a user by username.

.. admonition:: Tip

   At this point, re-starting your application will not change the view
   at ``localhost:8080``, but you can confirm you have done everything correctly if you see a ``user`` 
   table in MySQL Workbench. 
   

.. _auth_studio_forms:

Create the Login and Registration Forms
---------------------------------------

#. Create an ``AuthenticationController``.

   #. Include an autowired ``UserRepository``.

#. Add session handling utilities. This includes:

   #. A static final variable for the session key.
   #. A method to get the user information from the session.
   #. A method to set the user in the session.

#. Create two DTOs for the user registration and login forms in a new package, ``dto`` under ``models``.

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
      #. Redirect the user to the login form.

.. admonition:: Tip

   Now, clicking the *Logout* navbar link will result in a redirect to the login page. You can also now create 
   a brand new user through the link to register as one, and confirm the object's existence in your ``user``
   table.

.. _auth_studio_filter:

Filter Requests
---------------

#. Create an ``AuthenticationFilter`` class in the ``javawebdevtechjobsauthentication`` package.

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

#. Register the filter with Spring.

   #. Create a class called ``WebApplicationConfig`` at the same 
      level as ``AuthenticationFilter`` with the following:

      .. sourcecode:: java
         :lineno-start: 11

         @Configuration
         public class WebApplicationConfig implements WebMvcConfigurer {

            // Create spring-managed object to allow the app to access our filter
            @Bean
            public AuthenticationFilter authenticationFilter() {
               return new AuthenticationFilter();
            }

            // Register the filter with the Spring container
            @Override
            public void addInterceptors(InterceptorRegistry registry) {
               registry.addInterceptor( authenticationFilter() );
            }

         }

.. admonition:: Tip

   You'll know your filter setup works when you re-start your application and attempt to get to 
   ``localhost:8080`` but instead get redirected to ``/login``.

   You'll also know that your filters are working if hitting your login and and register forms now renders
   them without any styling. Bonus points if you can determine why this is.


That's it, that's all. You're done. Go forth and test the auth flow. 
Then add this to any other Spring project you're working on!
      
