Controllers
===========

The first of the MVC elements we'll work on implementing are the controllers. Recall that controllers 
are like the traffic cops of our application. They handle the requests and move data accordingly.

Create a Controller for your Spring Boot Project
------------------------------------------------

#. First, go to *src->main->java* and right click on your
   ``org.launchcode`` package and then select *New->Package* and name
   your new package ``controllers``.
#. Add a *New->Java Class* to the package ``controllers`` and name it
   ``HelloController``.
#. Above the class definition for ``HelloController``, add the annotation
   ``@Controller`` and add the corresponding class to your project.
#. Add this code to the body of your ``HelloController`` class:

.. sourcecode:: java
   :linenos:

   @RequestMapping(value="")
   @ResponseBody
   public String index() {
      return "Hello World";
   }

#. Use Gradle to *bootRun* again and visit *localhost:8080*. You should
   see “Hello World”
#. Now add another controller at another path by adding this code below
   the code posted above:

.. sourcecode:: java
   :linenos:

   @RequestMapping(value="goodbye")
   @ResponseBody
   public String goodbye(){
      return "Goodbye";
   }

#. Run the application again and visit *localhost:8080/goodbye* and you
   should see “Goodbye”.

Congratulations! You just ran your first Spring Boot program in
IntelliJ!

.. tip::

   IntelliJ has a lot of helpful keyboard shortcuts. You saw me use
   ``option + return`` (or ``alt + enter`` on Windows and Linux) in this
   video. Find out more
   `here <https://www.jetbrains.com/help/idea/2017.1/keyboard-shortcuts-you-cannot-miss.html>`__.


.. |windows bootRun| image:: images/windowsBootRun.png

