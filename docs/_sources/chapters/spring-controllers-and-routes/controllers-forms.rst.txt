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

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: No one controller method can handle several request types.
 
   a. True
      
   b. False

.. ans: b, A controller method annotated with @RequestMapping can handle multiple request types

.. admonition:: Question

   We want the method ``hello`` to take another parameter, ``@RequestParam String friend``, that will 
   add a friend's name to the returned greeting. The use should also be able to enter this name via 
   a text field. What needs to be added to the form?
 
   a. Another ``input`` tag with a ``friend`` attribute.

   b. Another ``input`` tag with a ``name`` attribute.

   c. Another ``form`` tag with a ``method`` attribute.

   d. Another ``submit`` tag with a ``friend`` value.

.. ans:  b, Another ``input`` tag with a ``name`` attribute.