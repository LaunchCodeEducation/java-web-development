Setup For Java
===============

For the entirety of this course, we will be coding in Java. We need to not only have
Java installed on our machines, but also some accompanying technologies to allow
us to run and edit our Java code.

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

A step-by-step walk-through of the process:

We write code in Java, the code is passed through the compiler program, which 
translates Java into **bytecode**, a language readable by the JVM. In the JVM,
bytecode is translated to machine code, which is then executed by your computer.

The JVM gives Java more flexibility than other compiled programming languages because
it will translate bytecode into the appropriate machine code, depending on the 
operating environment.


Install the JDK
---------------

In order to learn Java, you need to have the JDK installed on your computer. 

Open a terminal window on your machine and enter the following command:

.. sourcecode:: bash

   java -version

If the response returns a version 13 or higher, you can move on to the section below,
:ref:`cli-java`.

If you do not have a version of Java at 13 or higher, you can download 
it `here <https://www.oracle.com/technetwork/java/javase/downloads/jdk13-downloads-5672538.html>`__.
The relevant install link is on the bottom of the page:

.. figure:: figures/installJava.png
   :alt: Install Java

   Install Java

To install, you must first select *Accept License Agreement*, then select any of 
the file type options for your operating system. Once you have completed the 
installation steps, return to your terminal and enter ``java -version`` again to 
ensure Java has been installed.

.. _cli-java:

CLI Java
--------

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

Java version 11 introduced the capability to compile single-file Java programs
without explicitly running a command to compile. If our ``Hello, World`` program
were more complex and contained another file, we would need to first run ``javac HelloWorld.java``,
to compile, followed by ``java HelloWorld.java``.


Install IntelliJ
-----------------

IntelliJ is an **integrated development environment (IDE)**. An IDE is like a text
editor on steroids. It's a program to not only write and edit your code, but an IDE
can also contain many other features to enhance the coding experience. IntelliJ offers
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

You've installed IntelliJ and you're ready to start exploring its many features.

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
   some of the Java project scaffolding to save us some time with infrastructure. 

   .. figure:: figures/projectTemplate.png
      :alt: Select project template

      Select project template

#. On the next window, enter ``HelloWorld`` for the name of the project.
   Click on the "3-dot" button to select a location to save the project. Here you can
   choose you Java projects folder you created in step one. Leave the base package as
   ``com.company``.

   .. figure:: figures/newProjectName.png
      :alt: New project window for IntelliJ

      Create the ``HelloWorld`` project in you Java projects folder.

#. Click *Finish* to create the project.

Hello World
^^^^^^^^^^^^


