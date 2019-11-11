Install Spring
==============

Spring Boot is a framework used to build Java web applications that
implement the
`MVC <https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488>`__
pattern. For more about Spring, check out `Spring
IO <https://spring.io/>`__.

Initialize a Spring Boot Project
--------------------------------

#. Go to `start.spring.io <https://start.spring.io/>`__.
#. For *Project*, select *Gradle Project*.
#. For *Language*, select *Java*.
#. For *Spring Boot*, select *2.2.x* (that is, the most
   recent 2.2 non-SNAPSHOT release).
#. For *Project Metadata/Group*, enter ``org.launchcode``.

   .. note::

      You can use whatever package name you want here. The convention is
      ``topleveldomain.domainname``. In other words, the reverse of what
      you would see in a URL.

#. For *Project Metadata/Artifact*, enter ``hello-spring``.

   .. note::

      This is the title of your project.

#. For *Project Metadata/Options/Java*, select *13*.
#. For *Dependencies*, search for and add the following: *Spring Web*,
   *Thymeleaf*,and *Spring Boot DevTools*.
#. Click *Generate* to create a ``.zip`` file of the project starter code.

.. figure:: figures/spring-initializr.png
   :alt: Spring initializr with options

   Spring Initializr with desired options selected.

Spring in IntelliJ
------------------

#. Move the downloaded unzipped folder from your downloads folder into
   another location such as ``LC101`` or your home directory.
#. Start IntelliJ.
#. Select *Import Project* and browse to where you put the downloaded
   project.
#. Select *Create project from existing sources* and all other defaults
   as you create the project.

   .. note::

      If you encounter an alert that the selected folder is not empty, choose
      the option to overwrite it.

#. If you see an Gradle build popup, go ahead and click
   *Import Gradle Project*.
#. If a window then opens, check the *Use auto-import* box and
   leave everything else as it is.

.. figure:: figures/import-gradle-tip.png
   :alt: Popup to import Gradle

   A popup to suggest importing Gradle.

.. admonition:: Note

   You may see a pop-up in the lower left-hand corner in your *Event Log*
   that reads: *Unindexed remote maven repositories found*.

   1. Select *Open repositories list* in the Event Log message. This will
      open the *Preferences* (or *Settings* for Windows users) window to
      *Build, Execution, Deployment > Build Tools > Maven > Repositories* .
   2. Select the Maven repository (https://repo1.maven.org/maven2) and
      click *Update* on the side.   

.. warning::

   This update usually takes about 20 minutes but can last up to an hour.

The Spring Project Structure
----------------------------

The Spring Initializr gives us a number of helpful files and
directories to get our Spring project up and running.

Within the ``src`` directory, you’ll find a familiar setup with both a ``main`` and
``test`` directory. Inside of ``main`` will be a ``java`` folder to house your packages and
classes. You’ll also find that there is a ``resources`` folder in ``main``. ``resources`` is
meant to hold your non-java code.

Outside of ``src``, a ``.gitignore`` contains the basic items of our project that
Spring expects to not be version controlled. These are files created by the IDE, the compiled
code in the ``.build`` directory, and the gradle ``.jar`` and directory.

Gradle
^^^^^^

Gradle is a Java tool that handles much of the work related to building and deploying software
applications in Java. Your Spring project contains a file called ``build.gradle``. As with most new
tools, you do not need to know everything that this file does. For now, the takeaway is that
Gradle manages the external dependencies in our project.

Remember specifying the dependencies of the Spring project? Scroll down to the bottom of your
``build.gradle`` file and you will see these items specified in a structure called ``dependencies``.

.. sourcecode:: java
   :lineno-start: 22
   dependencies {
      implementation ‘org.springframework.boot:spring-boot-starter-thymeleaf’
      implementation ‘org.springframework.boot:spring-boot-starter-web’
      developmentOnly ‘org.springframework.boot:spring-boot-devtools’
      testImplementation(‘org.springframework.boot:spring-boot-starter-test’) {
         exclude group: ‘org.junit.vintage’, module: ‘junit-vintage-engine’
      }
   }

Gradle fetches these external packages from another location on the Internet so that we can use them
in our project locally. That location is called the Maven central repository. The Maven central repository
is a decentralized place for developers to post their code for others to use.

Running a Spring Project
------------------------

To run the application, click on the Gradle icon on the side of your IntelliJ window. If you don’t see the Gradle side bar, 
click the panel icon in the bottom left corner of your window and select *Gradle*. 

.. figure:: figures/panel-icon.png
      :alt: Panel icon options expanded

      Hovering over this icon opens options for panels to open.

Once the Gradle panel is opened, go into *Tasks->application* and double-click *bootRun*.

.. figure:: figures/gradle-bootrun.png
      :alt: Gradle panel view with bootRun selected

      Gradle panel view with bootRun selected.

.. admonition:: Note

   Also note that you may not see the same output in the Gradle panel as is
   shown in the video. You may see something that looks more like this:
   
   .. figure:: figures/windows-bootrun.png
      :alt: Alternative bootrun view

      Click the circled icon to switch the view.

   If you do, click the circled icon to toggle the view so that it matches
   the one in the video.

-  You can then visit the corresponding web page at ``localhost:8080``
   (Right now, you’ll see an error page, but we’ll fix that below.) Now
   go ahead and stop the application.

.. Create a Controller for your Spring Boot Project
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. -  First, add the necessary classes to your
..    *src->main->java->org.yourorgname->HelloSpringApplication*:
..    ``SpringBootApplication`` and ``SpringApplication``.
.. -  Next, go to *src->main->java* and right click on your
..    ``org.yourorgname`` package and then select *New->Package* and name
..    your new package ``controllers``.
.. -  Add a *New->Java Class* to the package ``controllers`` and name it
..    ``HelloController``.
.. -  Above the class definition for ``HelloController`` add the annotation
..    ``@Controller`` and add the corresponding class to your project.
.. -  Add this code to the body of your ``HelloController`` class:

.. .. code:: java

..        @RequestMapping(value="")
..        @ResponseBody
..        public String index(){
..            return "Hello World";
..        }

.. -  Use Gradle to *bootRun* again and visit *localhost:8080*. You should
..    see “Hello World”
.. -  Now add another controller at another path by adding this code below
..    the code posted above:

.. .. code:: java

..        @RequestMapping(value="goodbye")
..        @ResponseBody
..        public String goodbye(){
..            return "Goodbye";
..        }

.. -  Run the application again and visit *localhost:8080/goodbye* and you
..    should see “Goodbye”.

.. Congratulations! You just ran your first Spring Boot program in
.. IntelliJ!

.. .. raw:: html

..    <aside class="aside-pro-tip">

.. IntelliJ has a lot of helpful keyboard shortcuts. You saw me use
.. ``option + return`` (or ``alt + enter`` on Windows and Linux) in this
.. video. Find out more
.. `here <https://www.jetbrains.com/help/idea/2017.1/keyboard-shortcuts-you-cannot-miss.html>`__.

.. .. raw:: html

..    </aside>

.. .. |windows bootRun| image:: images/windowsBootRun.png




.. .. index:: ! mvc

.. MVC - design pattern. an approach to solving a common software problem. 
.. not specific to java or spring, but an abstract approach.

.. Models - buusiness objects. represent data that is part of the care functionality of the program. 
.. structure is independent from the framework.
.. ex - blog app - users are mdoels, so are blog posts

.. Views - display data to the user via an interface

.. controlloers - traffic cops. connect the model and views together. handle requests and move data

.. mvc flow

.. spring boot - one portion of a larger framework called spring
.. 	spring mvc is a module w/in 
.. 	boot is an extension of spring mvc
.. 	convention over configuration
.. 		embedded application server. tomcat
.. 		default settings and locations - dont have to configure every path or settings
.. 		easier configuration

.. start.spring.io - 11:25 time for spring initializr info

.. Hello Spring
.. ============

.. Spring Boot is a framework used to build Java web applications that
.. implement the
.. `MVC <https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488>`__
.. pattern. For more about Spring, check out `Spring
.. IO <https://spring.io/>`__. 



.. Some of the benefits of Spring Boot are:

.. -  Web development is simplified even more in Spring Boot than in Spring
.. -  It provides Tomcat as an embedded web server
.. -  A lot of settings are configured for us so there’s no need for
..    additional XML configuration



