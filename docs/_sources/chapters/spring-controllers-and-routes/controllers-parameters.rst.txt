.. index:: ! route, ! routing

Controllers with Parameters
===========================

Now that you kow the basics of a controller method, we can start to add some more variables into the mix. Some 
controller methods can take in parameters in the form of query strings or sections of the URL path. Passing
this URL data to the controller is one step closer to more flexible web applications. 

A **route** is the mechanism by which a request path gets assigned to a
controller within our application. We’ll explore routes
and how data is transferred from a webpage with a given route to a specific controller.

.. index:: ! query string

Query Strings are URL Data
--------------------------

A brief refresher: Query strings are additional bits of information tacked onto the ends of urls.
They contain data in key-value pairs.

.. sourcecode:: bash

   www.galaxyglossary.net?aKey=aValue&anotherKey=anotherValue&thirdKey=thirdValue

.. admonition:: Note

   Do HTTP requests and responses feel unfamiliar? Do you remember what a **query string**
   is? If you're feeling rusty on these topics, it's a good idea to brush up now, as routing 
   requires a foundational understanding of HTTP data transfer.

   Here's our `introduction to HTTP <https://education.launchcode.org/intro-to-professional-web-dev/chapters/http/index.html>`__ 
   for reviewing the concepts.

.. index:: ! @RequestParam

``@RequestParam``
-----------------

We can pass ``@RequestParam`` as an argument of a controller method. This annotation as an
argument lets the handler method know about a given query string based on its own argument.

.. sourcecode:: java

   // Responds to get requests at /hello?coder=LaunchCoder
   @GetMapping("hello")
   @ResponseBody
   public String hello(@RequestParam String coder) {        
      return "Hello, " + coder + "!";
   }

The controller method looks for the query string in the URL that matches its parameter, ``coder``, and puts
the paired value of that ``coder`` key into the response text.

.. index:: ! @PathVariable

``@PathVariable``
-----------------

Another way to handle data with a controller is by accessing the data via a segment of the 
URL. This is done with ``@PathVariable``. ``@PathVariable`` takes an argument that, if matching
a portion of the URL, will deliver this data into the handler.

.. sourcecode:: java

   // Responds to get requests at /hello/LaunchCode
   @GetMapping("hello/{name}")
   @ResponseBody
   public String helloAgain(@PathVariable String name) {
      return "Hello, " + name + "!";
      }	    
   }

Above, ``name`` is a placeholder, indicating where in the URL segment to look for the ``@PathVariable``. From 
the comment, we know that that the actual value is ``LaunchCode``, but this can easily be changed. If we changed
the value of this URL segment to ``/hello/Ada``, then this controller would respond with ``Hello, Ada`` when a 
``GET`` request is made.

.. note::

   Also know that you can redirect a user by removing the ``@ResponseBody``
   annotation from the controller and returning
   ``"redirect:/DESIREDPATH"``.


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