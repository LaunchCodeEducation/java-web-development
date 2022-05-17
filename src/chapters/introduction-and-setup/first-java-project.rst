.. _create-new-java-project:

Your First Java Project
=======================

Following the "Hello, World" trend, let's create a new IntelliJ project.

#. Create a new folder to hold your Java practice files. Since you will be
   creating lots of small projects as you move through this course, we
   suggest that you also add sub-folders with names corresponding to the
   related chapters and projects. Something like
   ``java-practice/chapter-name/project-name``.
#. Select the *New Project* option from the welcome screen.

   .. figure:: figures/IntelliJWelcome.png
      :scale: 70%
      :alt: Welcome window for IntelliJ. Select the New Project button.

      Start a new project

#. Clicking *New Project* opens a window with a series of project settings to
   select. This window is called the *new project wizard*.

   a. Choose *Java* from the options on the left in the project wizard.
   b. For *Project SDK*, you'll want to use version 11 that you have downloaded. 
      If **11** is not already selected in the SDK window, click *New* on the right and find the JDK you have just downloaded.
   
   The SDK allows IntelliJ to compile our Java code when we launch our
   programs. Click *Next* in the lower right corner of the window to continue
   selecting settings.

   .. figure:: figures/projectSDK.png
      :alt: Select project SDK

      Select project SDK

#. In the second window, select *Create project from template*. This gives us
   some of the Java project scaffolding to save us some time with project infrastructure. 

   .. figure:: figures/projectTemplate.png
      :alt: Select project template

      Select project template

#. On the next window, enter ``HelloWorld`` for the name of the project.
   Click on the "3-dot" button to select a location to save the project. Here you can
   choose the Java projects folder you created in step one. You do not need to change the
   base package.

   .. figure:: figures/newProjectName.png
      :alt: New project window for IntelliJ

      Create the ``HelloWorld`` project in your Java projects folder.

#. Click *Finish* to create the project. Below is the view of your new project.
   Click on the item labelled *Project* with an icon that looks like a file folder on the left of the project window.

   .. figure:: figures/newProjectView.png
      :alt: New project view

      Initial IntelliJ project view

   The section on the left is the project's **file tree**. 

   Clicking the triangle next to the project name, ``HelloWorld``, displays the ``src`` file, 
   followed by the base package we created, and finally our ``Main.java`` file. 
   
   ``Main.java`` is also opened on the right in this initial project view. 
   
   In line 1, ``package com.company``, establishes a *package*, which Java uses to help
   organize and encapsulate our code. 

#. We'll dive into the use of a ``main`` function and ``Main`` class later. At this point,
   let's just get right to printing our greeting. Where the project template tells you to write your
   code on line 6, add the following:

   .. sourcecode:: java

      System.out.println("Hello, world!");

   Ok sure, we haven't gone over this exact syntax yet. But you can take a guess at what this line will do.

#. To run your program in IntelliJ, you have several options.

   .. figure:: figures/runProgram.png
      :alt: Run code options

      IntelliJ run code options

   You can click on either of the green arrows indicated above, or 
   choose *Run* from your top menu bar.

#. Once run, IntelliJ will generate a third panel in your view, with your program's output:

   .. figure:: figures/output.png
      :alt: Run code output

      IntelliJ output

This is just the start of your relationship with IntelliJ. Now that we know the fundamentals,
let's return to Java basics so we can start writing more code.

Check Your Understanding
------------------------

.. admonition:: Question

   Given the code below, which line is responsible for printing a message?

   .. sourcecode:: java
      :linenos:

      public class HelloWorld {

         public static void main(String[] args) {
            System.out.println("Hello, World");
         }

      }

   #. line 1
   #. line 3
   #. line 4

.. admonition:: Question

   In the sourcecode above, which line is responsible for defining the class?

   #. line 1
   #. line 3
   #. line 4