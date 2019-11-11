Hello Spring
============

Spring Boot is a framework used to build Java web applications that
implement the
`MVC <https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488>`__
pattern. For more about Spring, check out `Spring
IO <https://spring.io/>`__. 



Some of the benefits of Spring Boot are:

-  Web development is simplified even more in Spring Boot than in Spring
-  It provides Tomcat as an embedded web server
-  A lot of settings are configured for us so there’s no need for
   additional XML configuration

Create a Simple Spring Boot Project
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Go to `start.spring.io <https://start.spring.io/>`__
-  Select *Gradle Project*, *Java*, and *1.5.x* (that is, the most
   recent 1.5 non-SNAPSHOT release) from the dropdown for “Generate a
   \__\_ with \__\_ and Spring Boot \__\_”
-  Put the title for your project, ``hello-spring``, in the section
   marked *Artifact*
-  Search for and add the following *dependencies*: Web, Thymeleaf,
   DevTools then click “Generate”
-  Move the downloaded unzipped folder from downloads into another
   location such as ``LC101`` or your home directory
-  Start IntelliJ
-  Select *Import Project* and browse to where you put the downloaded
   file
-  Select “Create project from existing sources”
-  Accept all defaults as you create the project
-  If you see an *Unlinked Gradle Project* popup, go ahead and click
   “Import Gradle Project”, then check the “Use auto-import” box and
   leave everything else as it is.

.. raw:: html

   <aside class="aside-note">

You may see a pop-up in the lower left-hand corner in your *Event Log*
that reads: **Unindexed remote maven repositories found**.

1. Select **Open repositories list** in the Event Log message. This will
   open the *Preferences* (or *Settings* for Windows users) window to
   *Build, Execution, Deployment > Build Tools > Maven > Repositories* .
2. Select the Maven repository (https://repo1.maven.org/maven2) and
   click *Update* on the side.

.. raw:: html

   </aside>

.. raw:: html

   <aside class="aside-warning">

This update usually takes about 20 minutes but can last up to an hour.

.. raw:: html

   </aside>

-  To run the application, click on the Gradle icon on the side, then go
   into *Tasks->application* and double-click *bootRun*

.. raw:: html

   <aside class="aside-note">

If you don’t see the Gradle side bar, click the panel icon in the bottom
left and select *Gradle*.

Also note that you may not see the same output in the Gradle panel as is
shown in the video. You may see something that looks more like this:
|windows bootRun|

If you do, click the circled icon to toggle the view so that it matches
the one in the video.

.. raw:: html

   </aside>

-  You can then visit the corresponding web page at ``localhost:8080``
   (Right now, you’ll see an error page, but we’ll fix that below.) Now
   go ahead and stop the application.

Create a Controller for your Spring Boot Project
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  First, add the necessary classes to your
   *src->main->java->org.yourorgname->HelloSpringApplication*:
   ``SpringBootApplication`` and ``SpringApplication``.
-  Next, go to *src->main->java* and right click on your
   ``org.yourorgname`` package and then select *New->Package* and name
   your new package ``controllers``.
-  Add a *New->Java Class* to the package ``controllers`` and name it
   ``HelloController``.
-  Above the class definition for ``HelloController`` add the annotation
   ``@Controller`` and add the corresponding class to your project.
-  Add this code to the body of your ``HelloController`` class:

.. code:: java

       @RequestMapping(value="")
       @ResponseBody
       public String index(){
           return "Hello World";
       }

-  Use Gradle to *bootRun* again and visit *localhost:8080*. You should
   see “Hello World”
-  Now add another controller at another path by adding this code below
   the code posted above:

.. code:: java

       @RequestMapping(value="goodbye")
       @ResponseBody
       public String goodbye(){
           return "Goodbye";
       }

-  Run the application again and visit *localhost:8080/goodbye* and you
   should see “Goodbye”.

Congratulations! You just ran your first Spring Boot program in
IntelliJ!

.. raw:: html

   <aside class="aside-pro-tip">

IntelliJ has a lot of helpful keyboard shortcuts. You saw me use
``option + return`` (or ``alt + enter`` on Windows and Linux) in this
video. Find out more
`here <https://www.jetbrains.com/help/idea/2017.1/keyboard-shortcuts-you-cannot-miss.html>`__.

.. raw:: html

   </aside>

.. |windows bootRun| image:: images/windowsBootRun.png



.. index:: ! mvc

MVC - design pattern. an approach to solving a common software problem. 
not specific to java or spring, but an abstract approach.

Models - buusiness objects. represent data that is part of the care functionality of the program. 
structure is independent from the framework.
ex - blog app - users are mdoels, so are blog posts

Views - display data to the user via an interface

controlloers - traffic cops. connect the model and views together. handle requests and move data

mvc flow

spring boot - one portion of a larger framework called spring
	spring mvc is a module w/in 
	boot is an extension of spring mvc
	convention over configuration
		embedded application server. tomcat
		default settings and locations - dont have to configure every path or settings
		easier configuration

start.spring.io - 11:25 time for spring initializr info



