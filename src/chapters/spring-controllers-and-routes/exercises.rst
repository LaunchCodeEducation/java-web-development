.. _controllers-exercises:

Exercises: Controllers and Routing
==================================

While reading the chapter, you created a
basic Hello, World application using Spring Boot called ``hello-spring``. Open that project up
in IntelliJ, and get ready to add some features!

.. admonition:: Note 

	Before your start these exercises, take a look at the 
	`hello-spring-demo class-annotations branch <https://github.com/LaunchCodeEducation/hello-spring-demo/tree/class-annotations>`__. 
	to make sure your own application matches ours.

Create and checkout a branch for your exercises solution. Name it something useful, such as ``controller-exercises``.

Modify your ``HelloController`` class to display a form on a ``GET``
request that asks the user for both their name and the language they
would like to be greeted in. It should look something like this:

.. figure:: figures/form.png
   :alt: Greeting Form

   Greeting Form

The resulting form submission should return and display the message,
“Bonjour Chris”.

.. admonition:: Note

   The language is presented in a dropdown, more formally known
   as a ``select`` element. For more information about the ``select`` element and how it works, read the `MDN documentation <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select>`__.

When the user submits the form (via a ``POST`` request), they should be
greeted in the selected language. Your new feature should: 

#. Include at least 5 languages, with English being the default. If you don’t speak 5 languages yourself, ask your friend `the Internet <http://pocketcultures.com/2008/10/30/say-hello-in-20-languages/>`__.
#. Include a new ``public static`` method, ``createMessage``, in the ``HelloController`` that takes a name as well as a language string. Based on the language string, you’ll display the proper greeting.

:ref:`Check your solution <controllers-exercise-solutions>`

Commit your changes!

Bonus Mission
-------------

#. Instead of returning the greeting as plain text, add a bit of HTML to
   the response string so that the displayed message looks a bit nicer.