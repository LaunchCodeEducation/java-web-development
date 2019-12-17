Setup For Java
===============

For the entirety of this course, we will be coding in Java. Besides installing Java on your machine, you must also add some support technologies to 
allow you to run and edit Java code.

.. index:: ! Java Development Kit, JDK, javac, Java Virtual Machine, JVM

Java Development Kit
--------------------

Installing Java means downloading a package of software called the **Java Development Kit**,
or **JDK**, for short. The JDK contains software the tools needed to develop and
run Java code, namely the the Java compiler, **javac**, and the 
**Java Virtual Machine (JVM)**. 

While the compiler is responsible for processing Java code into machine readable
code, the JVM allows us to run that code on any computer. These tools 
together, downloaded as the JDK, give us the means to write, compile, and run Java
on our machines.

.. _compiling-java:

A step-by-step walk-through of the process:

.. index:: ! bytecode

#. We write code in Java, 
#. The code is passed through the compiler program, 
#. The compiler translates Java into **bytecode**, a language readable by the JVM. 
#. In the JVM, bytecode is translated to machine code, 
#. Your computer then reads and executes the machine code.

The JVM gives Java more flexibility than other compiled programming languages because
it will translate bytecode into the appropriate machine code, depending on the 
operating environment.


Install the JDK
---------------

Open a terminal window on your machine and enter the following command:

.. sourcecode:: bash

   java -version

If the response returns a version 13 or higher, you can move on to the section below,
:ref:`terminal-java`.

If you do not have a version of Java at 13 or higher or the command does not work, you can download 
it `here <https://www.oracle.com/technetwork/java/javase/downloads/jdk13-downloads-5672538.html>`__.
The relevant install link for your operating system is on the bottom of the page:

.. figure:: figures/installJava.png
   :alt: Install Java

   Install Java

To install, you must first select *Accept License Agreement*, then select any of 
the file type options for your operating system. 

.. tip::

   - Mac users, we recommend the ``.dmg`` option
   - Windows users, we recommend the ``.exe`` option

Once you have completed the 
installation steps, move onto the next section.

.. admonition:: Note

   When installing Java on Windows, the installer will tell you where it wants to install Java.
   The default is in the C: Drive under ``Program Files``. Make note of the destination as we will be using it later.

.. _terminal-java:

Java in the Terminal
--------------------

Mac Users
^^^^^^^^^

Let's write a simple "Hello, World" program and watch the JDK in action. 

In the future, we'll be doing most of our Java coding with the IntelliJ IDE. 
IntelliJ contains many features to help us write Java properly and easily, 
including its own compiler. For now though, we'll use a simpler text editor 
so we can demonstrate what we get with the JDK.

In the text editor of your choice, create and save a file called 
``HelloWorld.java`` and include the code below:

.. sourcecode:: java
   :linenos:

   public class HelloWorld {

      public static void main(String[] args) {

         System.out.println("Hello, World");
      }

   }

We'll discuss the syntax of this program soon, but you can likely trust your gut
that this program has an expected output of "Hello, World". To test this hypothesis,
open a terminal window and navigate to the parent directory of your new file. Run:

.. sourcecode:: bash

   java HelloWorld.java

You should see your greeting printed! 

Recall from the walk-through :ref:`above <compiling-java>`, Java needs to be be compiled before executing. Java version 11 introduced 
the capability to compile single-file Java programs without explicitly running a command to compile. If our 
``Hello, World`` program were more complex and contained another file, we would need to first run 
``javac HelloWorld.java``, to compile, followed by ``java HelloWorld.java``.

Windows Users
^^^^^^^^^^^^^

Let's write a simple "Hello, World" program and watch the JDK in action. 

In the future, we'll be doing most of our Java coding with the IntelliJ IDE. 
IntelliJ contains many features to help us write Java properly and easily, 
including its own compiler. For now though, we'll use a simpler text editor 
so we can demonstrate what we get with the JDK.

In the text editor of your choice, create and save a file called 
``HelloWorld.java`` and include the code below:

.. sourcecode:: java
   :linenos:

   public class HelloWorld {

      public static void main(String[] args) {

         System.out.println("Hello, World");
      }

   }

We'll discuss the syntax of this program soon, but you can likely trust your gut
that this program has an expected output of "Hello, World". 

To test this hypothesis, open a terminal window and navigate to the parent directory of your new file.
In a separate window, navigate to the ``bin`` folder in the Java Development Kit to get the file path (the image below shows you how to get there from the C: Drive). Copy the file path.

.. figure:: figures/windowsjavafilepath.png
   :alt: Image showing that the JDK can be found inside the Program Files directory in the C: Drive.

Run the following command, replacing the ``{filepath}`` with the file path to your JDK that you just copied:

.. sourcecode:: bash

   set path=%path%;{filepath}

This command sets a path in our system for ``java`` so that we can compile and run Java programs.

.. sourcecode:: bash

   java HelloWorld.java

You should see your greeting printed! 

Recall from the walk-through :ref:`above <compiling-java>`, Java needs to be be compiled before executing. Java version 11 introduced 
the capability to compile single-file Java programs without explicitly running a command to compile. If our 
``Hello, World`` program were more complex and contained another file, we would need to first run 
``javac HelloWorld.java``, to compile, followed by ``java HelloWorld.java``.

.. admonition:: Note

   These steps change the path in just that directory.
   While this is sufficient to get us through the rest of the course, you may want change the system path for your whole system.
   Check out these `instructions <https://www.java.com/en/download/help/path.xml>`_ to change the path globally.

.. index:: ! integrated development environment, IDE

.. _install-intellij:

Install IntelliJ
-----------------

IntelliJ is an **integrated development environment (IDE)**. An IDE is like a text
editor on steroids. It not only allows you to write and edit code, but also contains many 
features that enhance the coding experience. IntelliJ offers
code completion hints, debugging, and even it's own compiler. We'll be using it throughout
this course, so it's time to get familiar with some of the basics.

Visit the `IntelliJ download site <https://www.jetbrains.com/idea/download/>`__.
Select your operating system and the Community version. Follow the installation
prompts to select your settings. When you reach the window asking for your UI theme,
you can choose to *Skip Remaining and Set Defaults*. You will finish on an IntelliJ
window listing the options to *Create New Project*, *Import Project*, *Open*, and 
*Check out from Version Control*.

.. figure:: figures/IntelliJWelcome.png
   :scale: 80%
   :alt: Welcome window for IntelliJ

   IntelliJ welcome window

You've installed IntelliJ, and you're ready to start exploring its many features.

.. _create-new-java-project:

Your First Java Project
------------------------

Following the "Hello, World" trend, let's create a new IntelliJ project.

#. Create a new folder to hold your Java practice files. Since you will be
   creating lots of small projects as you move through this course, we
   suggest that you also add sub-folders with names corresponding to the
   related chapters and projects. Something like
   ``java-practice/chapter-name/project-name``.
#. Select the *Create New Project* option from the welcome
   screen.

   .. figure:: figures/IntelliJWelcome.png
      :scale: 80%
      :alt: Welcome window for IntelliJ

      Create new project

#. Clicking *New Project* opens a window with a series of project settings to
   select. For this first setting, make sure your selected project SDK is the JDK
   you have installed. This allows IntelliJ to compile our Java code in-app. 
   Click *Next* in the lower right corner of the window to continue selecting settings.

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
   choose the Java projects folder you created in step one. Leave the base package as
   ``com.company``. 

   .. figure:: figures/newProjectName.png
      :alt: New project window for IntelliJ

      Create the ``HelloWorld`` project in your Java projects folder.

#. Click *Finish* to create the project. Below is the view of your new project:

   .. figure:: figures/newProjectView.png
      :alt: New project view

      Initial IntelliJ project view

   The section on the left is the project's file tree. 

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

This is just the start of your relationship with IntelliJ. Not that we know the fundamentals,
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


