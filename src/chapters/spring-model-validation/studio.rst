Studio: Spa User Validation
===========================

We’ll build on the :ref:`User Signup <user-signup-studio>` studio from last
class, adding in model validation.

Getting Started
---------------

Open up your ``spa-day`` application and checkout the `user-signup-pt2 <https://github.com/LaunchCodeEducation/spa-day-starter-code/tree/user-signup-pt2>`__ branch. 

Add Validation Annotations
--------------------------

Navigate to the ``User`` model class. Add `validation
annotations <https://docs.jboss.org/hibernate/beanvalidation/spec/2.0/api/>`__
to ensure these conditions are satisfied:

#.  Username, password, and verify are required (they can’t be empty)
#.  Username is between 5 and 15 characters
#.  Email is optional
#.  If provided, the email has the format of a valid email address.
#.  The password is at least 6 characters long

Using the Model to Render the Form
----------------------------------

In the ``UserController``, modify the ``add`` method that displays the
form so that it passes in an empty ``User`` object with:

.. sourcecode:: java

   model.addAttribute(new User());

This object will be accessible in the template, by name, as ``user``.

.. admonition:: Tip

   Now that you're passing in an empty ``User`` object, you may notice some redundant code
   in your ``processAddUserForm`` controller. Remove the model attribute additions
   and update the ``user/add`` template to make use of the model fields (eg. ``user.username``).

While you’re in the ``add.html`` template remove the ``type="email"`` designation from the email 
input. The last studio had you add this type to provide some client-side validation on the email
field, but we shouldn’t consider that sufficient. Now that we know how to use model validation to 
validate an email field, we'll favor this technique over client-side validation. Even with client-side 
validation (that is, in the browser), you should always validate data on
the server as well. You might want to provide constraints in addition to
or beyond what the browser does, and it’s also possible for a clever
(or, more often, malicious) user to bypass the browser’s validation. For this studio, we'll remove the 
input type to make it easier to test the server-side validation.


Validating Form Submission Data
-------------------------------

Now that you have your form set up, go back to ``UserController`` and
add validation on form submission by adding the ``@Valid`` annotation to
the ``User`` parameter that is bound, along with an additional
parameter: ``Errors errors``. 

.. admonition:: Warning 

   Remember, you must put this parameter directly
   after the ``User`` parameter in the method definition for it to work
   properly.

Within the ``processAddUserForm`` handler, check for errors configured by the
validation annotation using ``errors.hasErrors()``. If this returns
``true``, return the user to the form. 


Validating That Passwords Match
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As we mentioned above, we are not able to use Spring’s validation
machinery to validate that the two password fields match given the setup
we have here. Checking ``errors.hasErrors()`` will only tell us if there
are errors in other form data fields.

Last studio, we added some validation checks to make sure the password fields match.
Now we have two validation sections: one for the annotation-configured
validation (which checks ``errors.hasErrors()``), and one that checks
that the password fields match. Make sure they work in-sync with each
other to properly return to the form if any of the validation conditions
fail.

.. admonition:: Tip

   You can, in fact, validate that passwords match using annotations by
   taking a slightly more difficult approach than we’ve done here. We
   outline how to do so in the Bonus Mission section.


Test, Test, Test!
-----------------

You made a lot of changes! Be sure to thoroughly test them to make sure
everything works as expected.

Bonus Mission
-------------

Let’s set up our ``User`` class so we can validate that the password
fields match using annotations.

1. Add a ``private String verifyPassword`` field to ``User``, along with
   getters and setters.
2. Add a new method, ``private void checkPassword``, that compares
   ``password`` and ``verifyPassword``. If neither is ``null`` and they
   don’t match, then set ``verifyPassword = null``.
3. In both ``setPassword`` and ``setVerifyPassword``, call
   ``checkPassword`` *after* setting the given field.
4. Add ``@NotNull`` to the ``verifyPassword`` field with the error
   message: “Passwords do not match”.
5. Refactor the controller and ``add.html`` template to use the
   built-in, annotation-based validation instead of the manual password
   validation that we carried out previously. Be sure to update the
   verify field and label in the form to use the field on the ``User``
   class, and to remove ``String verify`` from the ``add`` method
   signature.

The result of these changes is that when the ``User`` object is bound to
the request, both ``password`` and ``verifyPassword`` are set. Spring
does this by calling the setters on these fields. The setters call
``checkPassword``, so when the second one is set (whichever that may
be), we’ll know that both ``password`` and ``verifyPassword`` are not
``null`` and we’ll compare them. If they don’t match, we manually
violate the ``@NotNull`` validation on ``verifyPassword`` by setting
that field to ``null``.