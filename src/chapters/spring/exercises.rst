Exercises: Bonjour Spring!
==========================

While reading the chapter, you created a
basic Hello, World application using Spring Boot called ``hello-spring``. Open that project up
in IntelliJ, and get ready to add some features!

Modify your ``HelloController`` class to display a form on ``GET``
request that asks the user for both their name and the language they
would like to be greeted in. It should look something like this:

.. figure:: figures/form.png
   :alt: Greeting Form

   Greeting Form

The resulting form submission should return and display the message,
“Bonjour Chris”.

.. admonition:: Note

   The language is presented in a dropdown, more formally known
   as a ``select`` element. For more information about ``select`` elements and how it works, read the `MDN documentation <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select>`__.

When the user submits the form (a ``POST`` request), they should be
greeted in the selected language. Your new feature should: 

#. Include at least 5 languages, with English being the default. If you don’t speak 5 lanugages yourself, ask your friend `the Internet <http://pocketcultures.com/2008/10/30/say-hello-in-20-languages/>`__.
#. Include a new ``public static`` method, ``createMessage``, in the ``HelloController`` that takes a name as well as a language string. Based on the language string, you’ll display the proper greeting.

Bonus Missions
--------------

#. Instead of returning the greeting as plain text, add a bit of HTML to
   the response string so that the displayed message looks a bit nicer.
#. Restructure your code so that the controller class doesn’t know
   anything about the specific languages available. In other words, it
   asks the model for available languages to present to the user.