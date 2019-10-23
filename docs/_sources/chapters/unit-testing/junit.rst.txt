JUnit
=====

JUnit is a library that provides the classes, methods, and assertions
for writing and executing unit tests in Java. In this course, 
we use JUnit4. Although there are newer versions now available, 
JUnit4 is still popular and widely used.

Java Annotations
^^^^^^^^^^^^^^^^

.. index:: ! annotations

On the topic of unit testing, the annotation ``@Test`` is used to 
indicate that a public void method should be treated as a test case.

In Java, **annotations** are formalized bits of information about a program. They operate
somewhere between actual code syntax and a comment on the code. Annotations do not 
directly affect the code they annotate, but they can supply information to the compiler.
Annotations are indicated with a ``@`` symbol. We will provide an example in the 
walkthrough below.


Testing Walkthrough
^^^^^^^^^^^^^^^^^^^

In your ``java-web-dev-exercises`` repo, we've included two ``.jar`` files for the JUnit 
library. These are located in the ``lib`` folder. In the future, as you build your own
Java projects, you will likely include these dependencies in a different fashion. Many Java
projects use a build automation tool to help manage dependencies, but since this project 
doesn't use one of these tools, we've included the ``.jar`` files.

``main/Car`` and ``test/CarTest``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Within ``org.launchcode.java.demos``, open the ``testing`` directory. Inside ``testing``, you'll
see a ``main`` directory and and ``test`` directory. Open the ``Car`` class within ``main`` and 
look around. Here, we provide a class ``Car`` with basic information about a make, model, 
gas level, and mileage as well as getters, setters, and a few other methods. 

In the same directory, you'll find a ``Main`` class with a main method that prints the
``make`` and ``model`` of a given ``Car`` object. Run this class to verify it works.
Now, open ``test/CarTest``. It's empty, save for a few TODOs. First, let's tackle the
first TODO to make a new emptty test. Starting with an empty test lets us validate that we can 
add JUnit to our classpath, and that the test can be run.

``@Test``
^^^^^^^^^

Create the following empty test underneath the first TODO. As usual,
be sure write this code rather than copy/paste it:

.. sourcecode:: java
   :linenos:

   //TODO: add emptyTest so we can configure our runtime environment
   @Test
   public void emptyTest() {
      assertEquals(10,10,.001);
   }

Once written, you likely have one of two states in your IntelliJ environment now. 
Either IntelliJ sensed which testing library you want to use and added the necessary 
import statements at the top of your class file. Or, IntelliJ flagged the ``@Test``
and ``assertEquals`` lines with red underlines, signalling to you the programmer to 
to add the necessary import statements.
Aren't :ref:`IDEs <install-intellij>` wonderful? 
If IntelliJ has added the import statements for you, make sure they
are the correct paths. Your import statements should look like:

.. sourcecode:: java

   import org.junit.Test;
   import static org.junit.Assert.assertEquals;

If these have not already been added to your file, add them now. As we mention above,
``@Test`` annotates the method to signal it as a test case. We need to add the appropriate
classpath in order to take advantage of this annotation. Our empty test is aptly named
``emptyTest()``, a description of its role. This test does not follow the AAA rule from 
our :ref:`testing-best-practices`, as it jumps straight to asserting.

Get the JAR
~~~~~~~~~~~

Download the `junit.jar <https://search.maven.org/search?q=g:junit%20AND%20a:junit>`__ 
and it's dependency, `hamcrest-core <https://search.maven.org/artifact/org.hamcrest/hamcrest-core/1.3/jar>`__.

Project Config Settings
~~~~~~~~~~~~~~~~~~~~~~~

Place tests in the correct location within a Java project
Add JUnit 4 to the project classpath
Group related tests together within the same class
Use the @Test annotation to mark a test method
Use @Before to generate test data to be used by each test within a class
Understand the behavior of @After
Run JUnit tests as a group, or individually, within IntelliJ
Use common assertion methods: assertEquals, assertFalse, assertTrue, assertNotNull

