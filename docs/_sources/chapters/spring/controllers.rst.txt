Controllers
===========

The first of the MVC elements we'll work on implementing are the controllers. Recall that controllers 
are like the traffic cops of our application. They handle the requests and move data accordingly. 
Here, we create two controllers. One handles requests to our index path, ``/``, another to a new path.

Create a Controller
-------------------

#. First, go to *src->main->java* and right click on your
   ``org.launchcode`` package and then select *New->Package* and name
   your new package ``controllers``.

#. Add a *New->Java Class* to the package ``controllers`` and name it
   ``HelloController``.

.. index:: ! @Controller

3. To tell the application that this class will function as a controller, add the annotation
   ``@Controller`` above the class definition for ``HelloController``. As always, be sure to 
   also add the corresponding class to your project.

   .. sourcecode:: java
      :lineno-start: 5

      @Controller
      public class HelloController {
      }

   .. note::

      Recall that annotations are like metadata about your code. They can help the framework do 
      its work by adding context to your code.

#. Inside of the class, we want to write a method that will return a ``Hello World`` message.

   Add this code to the body of your ``HelloController`` class:

   .. sourcecode:: java
      :lineno-start: 8

      public String index() {
         return "Hello World";
      }
   
   We've called this method ``index`` because it will be mapped to the index page, ``/`` of 
   our application.

.. index:: ! @RequestMapping

5. To specify which path this method is associated with, we add another annotation, 
   ``@RequestMapping``.

   .. note::
   
      For every controller method that you want to respond to a request, you will use this 
      ``@RequestMapping`` annotation.

   Add the annotation above your method:

   .. sourcecode:: java
      :lineno-start: 9

      @RequestMapping(value="")
      public String index() {
         return "Hello World";
      }

   Here, ``value=""`` tells the controller that we are mapping this method to the default path, "".

.. index:: ! @ResponseBody

6. To return the text of our method, ``Hello World``, we need to add one more annotation to this method,
   ``@ResponseBody``.

   .. sourcecode:: java
      :lineno-start: 10

      @RequestMapping(value="")
      @ResponseBody
      public String index() {
         return "Hello World";
      }

   .. note::
   
      Soon, we'll begin returning data in template contexts. Until then, we need the 
      ``@ResponseBody`` annotation to handle returning plain text.
      

#. Use Gradle to *bootRun* again and visit *localhost:8080*. You should
   see your message, “Hello World”.

#. Now, lets add another controller method that maps to a non-default path.
   Anywhere inside your class, add:

   .. sourcecode:: java
      :lineno-start: 16

      @RequestMapping(value="goodbye")
      @ResponseBody
      public String goodbye(){
         return "Goodbye";
      }

   In this method, the value on ``@RequestMapping`` is the path that this request is affiliated 
   with. We've also named the method with the same name, but this equality is not necessary, just 
   helpful.

#. Run the application again and visit *localhost:8080/goodbye* and you
   should see “Goodbye”.

Congratulations! You can write controllers!

.. tip::

   IntelliJ has a lot of helpful keyboard shortcuts. Find out more
   `here <https://www.jetbrains.com/help/idea/2017.1/keyboard-shortcuts-you-cannot-miss.html>`__.


