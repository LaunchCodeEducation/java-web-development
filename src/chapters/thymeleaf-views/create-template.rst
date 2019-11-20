Creating a Template
====================

Using templates is a useful way to reduce the effort required to create and
maintain a web-based project. Before you can dive into using templates,
however, you need to take care of a little groundwork first.

Thymeleaf
----------

.. index:: ! Thymeleaf

In combination with Java and Spring Boot, we will use a library called
**Thymeleaf**. This set of tools helps simplify the creation of flexible,
reusable templates for standalone projects and web-based applications.

More information can be found on the `introduction page <https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#introducing-thymeleaf>`__
of the Thymeleaf website.

Thymeleaf, Naturally
^^^^^^^^^^^^^^^^^^^^^

The developers behind Thymeleaf emphasize the idea of *natural templates*. This
means that templates constructed with Thymeleaf look and operate just like
regular HTML code. You can open any template in a browser and view it just
like a static HTML file.

Any logic we add to a template occurs inside the tags, which preserves the
ability to open the file and display it correctly. This helps us as we
develop the framework for presenting data on the screen.

Thymeleaf Dependency
---------------------

In this chapter, you will construct a small practice project to help you learn
how to implement Thymeleaf templates. To use the library, however, you need to
provide IntelliJ with some information to make the IDE recognize Thymeleaf
syntax and commands. You need to include in the proper *dependencies*, and
there are two common ways to accomplish this.

During Setup for a New Project
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When you create a new Gradle project on the `start.spring.io <https://start.spring.io/>`__
website, search for and select the *Thymeleaf* dependency. For the practice
projects you build in this class, be sure to add the *Spring Web* and
*Spring Boot DevTools* dependencies as well.

.. figure:: ./figures/selectTLdependency.png
    :alt: Select the Thymeleaf dependency.

In IntelliJ, opening up the ``build.gradle`` file of the new project shows the
dependencies you selected:

.. sourcecode:: groovy
   :lineno-start: 22

   dependencies {
      implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
      implementation 'org.springframework.boot:spring-boot-starter-web'
      developmentOnly 'org.springframework.boot:spring-boot-devtools'
      testImplementation('org.springframework.boot:spring-boot-starter-test') {
         exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
      }
   }

Lines 23 - 25 establish links to the thymeleaf, spring-boot-starter-web, and
spring-boot-devtools libraries, respectively.

Add to an Existing Project
^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you have an existing project that does not currently use Thymeleaf, you
can add the functionality by updating the ``build.gradle`` file.

.. figure:: ./figures/buildGradleFileTree.png
   :alt: Open the ``build.gradle`` file.

In the ``dependencies`` block, just paste in the ``implementation`` statement
seen in line 23 above. Also, be sure to include the Spring Boot libraries if
the old project is missing those as well.

Start a Practice Project
-------------------------

Rutabagas...

Add a Template
^^^^^^^^^^^^^^^

Lorem ipsum...

Template Location
^^^^^^^^^^^^^^^^^^

Lorem ipsum...

Check Your Understanding
-------------------------

Questions go here...
