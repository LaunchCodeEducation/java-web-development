Setup For Java
==============

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

If the response returns a major version 11 (ie 11.0.0 or higher, but not as high as 12.0.0), you can move on to the section below,
:ref:`terminal-java`.

If you do not have Java 11, or the command does not work, you can download 
it `here <https://www.oracle.com/java/technologies/javase-jdk11-downloads.html>`__.
The relevant install link for your operating system is on the bottom of the page:

.. figure:: figures/installJava.png
   :alt: Screenshot of different Java installation options on Oracle's website

   The figure above shows options for downloading Java 15. You should download Java 11 from the link above.

- **Mac users**: we recommend the ``.dmg`` option
- **Windows users**: we recommend the ``.exe`` option

To install, you must first select *Accept License Agreement*. 

Make note of the location where the Java JDK has been installed on your computer. 

- **Mac users**: This should be ``/Library/Java/JavaVirtualMachines``.

- **Windows users**: This should be in the C: Drive under ``Program Files``

Once you have completed the installation steps, move onto the next section.

