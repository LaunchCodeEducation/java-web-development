Routes Walkthrough
==================

Data Transfer by ``GET``
------------------------

Pass in an argument 

#. Add to your controller a parameter that is a request object of the
   ``HttpServletRequest`` class.
#. Get data from this request object by using the key of the desired
   parameter and the method ``getParameter``.
#. Use the data in your controller to return a customized greeting.

.. sourcecode:: java

   @RequestMapping(value = "")
   @ResponseBody
   public String index(HttpServletRequest request){
      String name = request.getParameter("name");
      return "Hello " + name;
   }

Data Transfer by ``POST``
-------------------------

#. Display a form that will allow the user to submit data. To do this,
   create a new request handler that returns a string of HTML.

.. sourcecode:: java

   @RequestMapping(value = "hello", method = RequestMethod.GET)
   @ResponseBody
   public String helloForm(){
      String html = "<form method='post'>" +
               "<input type='text' name='name' />" +
               "<input type='submit' value='Greet Me!'/>" +
               "</form>";
      return html;
   }

#. Create another handler that will handle ``POST`` requests and access
   the request object.

.. sourcecode:: java

   @RequestMapping(value = "hello", method = RequestMethod.POST)
   @ResponseBody
   public String helloPost(HttpServletRequest request){
      String name = request.getParameter("name");
      return "Hello " + name;
   }

Data Transfer by URL Segment
----------------------------

#. Create a new handler that will access data via a URL segment:

.. sourcecode:: java

   @RequestMapping(value = "hello/{name}")
   @ResponseBody
   public String helloUrlSegment(@PathVariable String name){
      return "Hello " + name;
   }

.. note::

   Also know that you can redirect a user by removing the ``@ResponseBody``
   annotation from the controller and returning
   ``"redirect:/DESIREDPATH"``.
