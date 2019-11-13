Controllers
===========

The first of the MVC elements we'll work on implementing are the controllers. Recall that controllers 
are like the traffic cops of our application. They handle the requests and move data accordingly. 

Diagram
-------

.. index:: ! @Controller

``@Controller``
---------------

To designate a given class as a controller within the Spring framework,
we use the annotation ``@Controller``. Recall that :ref:`java-annotations` 
are like metadata about your code. They help the framework do 
its work by adding context to your code.

.. index:: ! @RequestMapping

``@RequestMapping``
-------------------

``@RequestMapping`` is another annotation used on both controller classes and methods. 
``@RequestMapping`` designates a controller action with a URL path. The path is defined with
``@RequestMapping(value="pathname")``. If the pathname value is null, then the path used is the 
index path, or ``/``.

For every controller method that you want to respond to a request, you will use this 
``@RequestMapping`` annotation. You may use it to designate a base path for a given controller class, 
but not every controller class needs a ``@RequestMapping`` annotation attached to it.

For example, say the URL of your Spring Boot application is ``galaxyglossary.net``. Your application 
catalogs items of various planetary galaxies. Above a controller class called ``MilkyWayController``, 
you have declared ``@RequestMapping(value="milkyway")``. Every method defined in this controller handles 
requests related to data on the Milky Way galaxy. All methods located here map to a base path of 
``galaxyglossary.net/milkyway``. ``MilkyWayController`` contains a method called ``orionArm()`` that 
is used to return data about the section of the Milky Way called Orion Arm. Above ``orionArm()`` is 
another ``@RequestMapping``, this one defined as ``@RequestMapping(value="orionarm")``. This means that 
anytime a user visits ``galaxyglossary.net/milkyway/orionarm``, the ``orionArm()`` method is used.


.. index:: ! @ResponseBody

``@ResponseBody``
-----------------

``@ResponseBody`` is yet another annotations used in the Spring controller context to return plain text
from a controller method. This annotation we will only need to use for a short while, before we start
to work with templates. Spring Boot's default action when responding to a controller method is to return 
a template. Since we aren't doing that yet however, we need to tell the framework to return plain tex by 
adding the ``@ResponseBody`` annotation.



Check Your Understanding
------------------------

.. admonition:: Question

   What is the name of the task to start a Spring Boot application?
 
   a. Gradle
      
   b. bootRun

   c. run

   d. Maven

.. ans: b, bootRun

.. admonition:: Question

   True/False: All custom code in a Spring Boot application goes in the main method.
 
   a. True

   b. False

.. ans: False, most features are developed outside of the main method.
