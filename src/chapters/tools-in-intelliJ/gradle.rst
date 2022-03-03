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

So far we have included Gradle in our project Spring Boot projects.  

.. admonition:: Note

   You can also import Gradle using the terminal. 
   Instuction on that is beyond the scope of this class, 
   but there is `documentation <https://spring.io/guides/gs/gradle/>`_ on this process if you are curious.


How Gradle Works
----------------

project > build scripts > tasks > plugins
stay VERY high level on this

A Gradle **project** contains all of the tasks, and plugins needed to build your application.
A **Task** is a single step required to build and run your application.  
Each task belongs to a **Project** and contains a sequence of 
**Action objects** that executes when called.  

When working with tasks, it is important to consider the order of execution.
It is also worth considering how tasks interact with one another as some may work independently
while others may rely on other tasks for proper execution.

You can create your own tasks for a project, or import tasks by using **plugins**.
Plugins contain all of the neccessary tasks and scripts to extend a project's capabilities.
You have worked with plugins already.  
In ``hello-spring`` and ``hello-spring-demo`` projects, the Spring Boot framework was added to our project as a plugin.

`More information <https://docs.gradle.org/current/userguide/plugins.html>`_ on using plugins in Gradle.

``build.gradle``
----------------

The ``build.gradle`` file is the project build script.  
This file holds any plugins, configurations, repositories, dependencies, and tests needed to run your project.
Gradle will refer to this file as it runs through the task list.

When you created your ``hello-spring`` project, Spring Boot flushed this file out for us.
Open your ``build.gradle`` file and look at each section.  
You should see a method called ``plugins``, which holds your plugins.

``configurations`` works with the ``dependencies`` method for 
https://medium.com/agorapulse-stories/gradle-configurations-explained-4b9608dd5e35 

``dependencies``
https://www.tutorialspoint.com/gradle/gradle_dependency_management.htm

``repositories``
https://www.tutorialspoint.com/gradle/gradle_dependency_management.htm 

https://tomgregory.com/gradle-dependency-tree/


Gradle Repositories
--------------------

text here
transistion here into Maven


Check Your Understanding
------------------------


here be questions




Each project is made up of **tasks**. 
A task is a single step needed for building our project.

Gradle comes with a collection of tasks, but you can add more tasks.
You can either create your own tasks by writing them or you can 
use pre-written ones called **plugins**.  
Plugins will typically automatically add its tasks, tests, and 
other packages to your application after installation.  
If you look at your Spring projects ``build.gradle`` file, 
you can see that the Spring Boot framework is a plugin.