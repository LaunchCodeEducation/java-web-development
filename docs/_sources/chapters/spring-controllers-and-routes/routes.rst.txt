Routes
======

A **route** is the mechanism by which a request path gets assigned to a
controller within our application. In this section, we’ll explore routes
and how data is transferred from a webpage to a specific controller.

We’ll look at three different ways controller methods handle data from users:

#. Via a ``GET`` request and query parameters 
#. Via a ``POST`` request and post parameters 
#. Via a URL segment and a path variable

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

``@RequestParam``
-----------------

We can pass ``@RequestParam`` as an argument of a controller method. This annotation as an
argument lets the handler method know about a given query parameter based on its own argument.

.. sourcecode:: java

   // Responds to /hello?name=LaunchCode
   public String hello(@RequestParam String name) {        
      return "Hello, " + name + "!";
   }

The controller method looks for the query string in the URL that matches its parameter, ``name``.

``@GetMapping`` and ``@PostMapping``
------------------------------------

In addition to ``value``, we can also give ``@RequestMapping`` another argument, ``method``,
where we declare which request type to use. This would look like:

.. sourcecode:: java

   @RequestMapping(value = "hello", method = RequestMethod.POST)


An alternative is to use ``@GetMapping`` or ``@PostMapping`` which declare the method type more directly. 
Of course, there are other annotations for the other request methods, but these are the two we will use in 
this class. These annotations behave just like ``@RequestMapping``, except that they cannot be applied to a 
whole class.


Data Transfer by URL Segment
----------------------------

Another way to handle data with a controller is by accessing the data via a segment of the 
URL. This is done with ``@PathVariable``. ``@PathVariable`` takes an argument that, if matching
a portion of the URL, will deliver this data into the handler.

.. sourcecode:: java

   // Responds to /hello/LaunchCode
   @GetMapping("hello/{name}")
   @ResponseBody
   public String helloAgain(@PathVariable String name) {
      return "Hello, " + name + "!";
      }	    
   }

.. note::

   Also know that you can redirect a user by removing the ``@ResponseBody``
   annotation from the controller and returning
   ``"redirect:/DESIREDPATH"``.

