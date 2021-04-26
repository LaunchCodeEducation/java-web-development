.. _controllers-exercise-solutions:

Exercise Solutions: Controllers and Routing
===========================================

When the user submits the form (via a ``POST`` request), they should be
greeted in the selected language. Your new feature should: 

#. Include at least 5 languages, with English being the default. If you don’t speak 5 languages yourself, ask your friend `the Internet <http://pocketcultures.com/2008/10/30/say-hello-in-20-languages/>`__.
#. Include a new ``public static`` method, ``createMessage``, in the ``HelloController`` that takes a name as well as a language string. Based on the language string, you’ll display the proper greeting.

.. sourcecode:: java

    @RequestMapping(value="hello", method = RequestMethod.POST)
    @ResponseBody
    public String helloPost(@RequestParam String name, @RequestParam String language) {
        if (name == null) {
            name = "World";
        }

        return createMessage(name, language);

        // For a bonus mission, students can change this response text to look nicer.
        // This is subjective, but students should be modifying the HTML of the response string.
    }

    public static String createMessage(String n, String l) {
        String greeting = "";

        if (l.equals("english")) {
            greeting = "Hello";
        }
        else if (l.equals("french")) {
            greeting = "Bonjour";
        }
        else if (l.equals("italian")) {
            greeting = "Bonjourno";
        }
        else if (l.equals("spanish")) {
            greeting = "Hola";
        }
        else if (l.equals("german")) {
            greeting = "Hallo";
        }

        return greeting + " " + n;
    }

:ref:`Back to the exercises <controllers-exercises>`