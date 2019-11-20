Controllers with Forms
======================

What if we want to send over some form data? To send data via a simple form in Spring 
Boot, we'll set things up like this:

We have a controller method that generates a form at index. 

.. sourcecode:: java

   @GetMapping
   @ResponseBody
   public String helloForm() {
      String html = 
         "<html>" +
            "<body>" +
               "<form method = 'get' action = '/hello'>" +
                  "<input type = 'text' name = 'coder' />" +
                  "<input type = 'submit' value = 'Greet Me!' />" +
               "</form>" +
            "</body>" +
         "</html>";
      return html;
   }

Remember, without an argument, ``@GetMapping`` maps to ``/``. On form submission, the 
data is sent to another path, ``/hello``. We need a controller for that.

.. sourcecode:: java

   @GetMapping("hello")
   @ResponseBody
   public String hello(@RequestParam String coder) {
      return "Hello, " + coder + "!";
   }

Now, you have a controller that can handle the form submission. When the form submits, the 
input entered in the text box will be passed to the URL via a query string. This is why 
the controller method above passes in ``@RequestParam`` to handle the ``coder`` key.

To be able to submit the form via ``POST``, we'll need to modify the ``hello()`` controller
to use ``@RequestMapping``. Remember, ``@RequestMapping`` can annotate a method that responds 
to both ``GET`` and ``POST``.

.. sourcecode:: java

   // Responds to get and post requests at /hello?coder=LaunchCoder
   @RequestMapping(value = "hello", method = {RequestMethod.GET, RequestMethod.POST})
   @ResponseBody
   public String hello(@RequestParam String coder) {        
      return "Hello, " + coder + "!";
   }

   @GetMapping
   @ResponseBody
   public String helloForm() {
      String html = 
         "<html>" +
            "<body>" +
               "<form method = 'post' action = '/hello'>" +
                  "<input type = 'text' name = 'coder' />" +
                  "<input type = 'submit' value = 'Greet Me!' />" +
               "</form>" +
            "</body>" +
         "</html>";
      return html;
   }




.. Check Your Understanding
.. ------------------------

.. .. admonition:: Question

..    What is the name of the task to start a Spring Boot application?
 
..    a. Gradle
      
..    b. bootRun

..    c. run

..    d. Maven

.. .. ans: b, bootRun

.. .. admonition:: Question

..    True/False: All custom code in a Spring Boot application goes in the main method.
 
..    a. True

..    b. False

.. .. ans: False, most features are developed outside of the main method.