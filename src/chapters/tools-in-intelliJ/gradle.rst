Gradle
======

.. index:: ! Gradle

By now you have created at least two Spring projects using Gradle.  
If you recall, Spring is the framework that will enable us to create an MVC application.
When we created each project, we selected "Gradle Project", but what is Gradle?

Gradle is an **automated build tool** that is responsible for tasks like:
   - Compiling source code
   - Managing Dependencies
   - Testing protocols
   - Packaging the executable program for deployment.

So far we have included Gradle in our Spring Boot projects.  

.. admonition:: Note

   You can also import Gradle using the terminal. 
   Instruction on that is beyond the scope of this class, 
   but there is `documentation <https://spring.io/guides/gs/gradle/>`_ on this process if you are curious.


How Gradle Works
----------------

A Gradle **project** contains all of the tasks, and plugins needed to build your application.
When you boot and run your Gradle project, it follows a build script that is contained in the ``build.gradle`` file.

``build.gradle``
^^^^^^^^^^^^^^^^

The ``build.gradle`` file is the project build script.  
This file holds any plugins, configurations, repositories, dependencies, and tests needed to run your project.
Gradle will refer to this file as it runs through the task list to build the application.  

.. admonition:: Note
   
   When you created your ``hello-spring`` and ``hello-spring-demo`` projects, 
   Spring Boot populated this file as the projects were initialized.
   Open your ``build.gradle`` file and look at each section.  


Gradle holds all plugins, tasks, dependencies, configurations, repos, 
and tests in methods, as needed, for better organization.  
To create your own or import from outside sources, you add code to the appropriate method.

``tasks`` and ``plugins``
^^^^^^^^^^^^^^^^^^^^^^^^^

Gradle builds a project by running **tasks**.
A task is a single step required to build and run your application.  
Each task belongs to a project and contains a sequence of action objects that execute when called. 

You can create your tasks for a project or import tasks by using **plugins** into the ``build.gradle`` file.
Plugins contain all of the necessary tasks and scripts to extend a project's capabilities.
Plugins will often require **dependencies** and external **repositories**.
You have worked with plugins already with your Spring Boot framework projects.

``dependencies``
^^^^^^^^^^^^^^^^

``dependencies`` are external libraries or artifacts of code that are needed to build your project.  
To keep ``dependencies`` organized, Gradle often groups related ``dependencies`` together in ``configurations``.
Often you will see the ``configuration`` name then ``dependency`` information. 

.. admonition:: Note

  Your ``hello-spring`` and ``hello-spring-demo`` projects each have three dependencies with three different configurations.

``configurations``
^^^^^^^^^^^^^^^^^^

Some projects contain a separate ``configurations`` method.  
This is another level of bundling dependencies within a project.  
In your ``hello-spring-demo`` project, the ``build.gradle`` file contains a ``configurations`` method. 
However, there are none in your ``hello-spring`` project.

.. admonition:: Note 

   In your ``hello-spring`` project, there is no separate configurations method.
   However, there is one in your ``hello-spring-demo`` project.

``repositories``
^^^^^^^^^^^^^^^^

If dependencies are external libraries, then where does the source code come from?
It comes from an external repository.  
In this class, we will be using Maven Central, a website containing files for any dependencies. 
Other repositories do exist and work similarly.

In the ``build.gradle`` file we link up with Maven Central by using the ``repositories`` method.


``tests``
^^^^^^^^^

This method holds any necessary configurations and 
dependencies for a certain test if using testing tasks.

.. admonition:: Note

   In your ``hello-spring`` and ``hello-spring-demo`` projects
   the ``build.gradle`` file was created by Spring Boot which 
   populated most of the file.

   This is not always the case depending on how you create a Gradle project.  

Troubleshooting Tips
--------------------

**My dependencies won't build**
   In this class, we are using IntelliJ as our IDE to build our Gradle projects.
   IntelliJ's built-in IntelliSense should prompt you to refresh your ``build.gradle`` 
   whenever you change the file.  You should see a small icon appear in the 
   top right corner of the ``build.gradle`` file.  If you click on the icon, it will
   refresh your build.  

   .. figure:: figures/gradle-refresh-point.png
      :alt: Gradle Refresh Icon

      The refresh icon should appear whenever you make changes to your project.

   However, if you update ``build.gradle`` and the icon does not appear, you can manually refresh the build.
   **Mac** Users try  *Shift + Command + I* and **Windows/Linux** Users: try *Control + Shift + O*.
   For more on Gradle and IntelliJ, visit this `website <https://www.jetbrains.com/idea/guide/tutorials/working-with-gradle/gradle-dependencies/>`_.

**I've refreshed, but they still won't build**
   If the refreshing above did not work, you can check out this 
   documentation on `Maven.Importing <https://www.jetbrains.com/help/idea/maven-importing.html>`_ 
   from IntelliJ. 

   If using 2019 IntelliJ, this article might offer some help.  `Check out tip #4 <https://tomgregory.com/5-tips-for-using-gradle-with-intellij-idea-2019/>`_.
   Not sure which version you are using look for the **About...** menu option to verify which version you are using.





Let's Recap
-----------

Gradle contains all code required to build an application.  
This includes code that you create as well as code from outside sources.
Gradle runs through each task, using code from you or external sources.
Tests the build and then packages it up for deployment.  
If everything goes to plan, you should have a functional application.


Check Your Understanding
------------------------

.. admonition:: Question

   From where do ``dependencies`` access their source code?
      a. An external repository such as Maven Central
      b. Internal code within a Class you created

   .. ans: a



