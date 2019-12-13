Thymeleaf Forms
================

Templates allow you to build generic forms. This lets you reuse the structure
by rendering the same template with different labels and data. Thus, a single
form can serve different purposes, saving you extra effort.

Whenever possible, reuse existing templates!

Start a New Project
--------------------

You will build a new project so you can practice with templates and forms.
If you have not done so, commit and push any unsaved work from your
``hello-spring`` project.

Your new project will keep track of some fictional coding events.

#. Use the `start.spring.io <https://start.spring.io/>`__ website to initialize
   your new project.
#. Follow the steps you used to setup
   :ref:`hello-spring <initialize-spring-boot-project>`, but call the new
   project ``coding-events``.
#. Be sure to add the *Thymeleaf* dependency in addition to *Spring Web*, and
   *Spring Boot DevTools*.

   .. figure:: ./figures/codingEventsInit.png
      :alt: Initialize ``coding-events`` project.
      :scale: 80%

#. *Generate* the ``.zip`` file and then import it into IntelliJ.

Try It!
--------

Now that you have ``coding-events`` up and running, add features to it by
coding along with the videos below:

.. raw:: html

   <div style="text-align:center;">
      <iframe width="800" height="450" src="https://www.youtube.com/embed/hmgxMOf51JU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
   </div>

.. raw:: html

   <div style="text-align:center;">
      <iframe width="800" height="450" src="https://www.youtube.com/embed/lgT962si4eQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
   </div>

Before moving on, be sure to commit and push your changes. Do this after each
video to create a fallback position just in case disaster strikes your project
in the future.

A summary of Thymeleaf forms is given below, but remember that the text
supports the videos and is NOT intended as a replacement.

Create and Render a Form
-------------------------

A Thymeleaf form is simply a template that includes a ``<form>`` element inside
the ``body`` of the HTML. The method for the form should be of type ``post``.

.. sourcecode:: HTML
   :linenos:

   <body>

      <!-- Other HTML -->

      <form method="post">
         <input type="text" name="inputName">
         <input type="submit" value="submitButtonText">
      </form>

      <!-- Other HTML -->

   </body>

You can include as many inputs as you need in the form, and these can be of
different types (e.g. text, email, checkbox, etc.). However, each different
piece of data you want to collect needs to have a unique ``name`` attribute.

To *render* the form in the view, add a method to the controller using the
``@GetMapping`` annotation:

.. sourcecode:: java
   :linenos:

   @GetMapping("formTemplateName")
   public String renderFormMethodName(Model model) {

      // Method code...

      return "pathToTemplate";
   }

Some points to note:

#. Line 1: The string parameter for ``GetMapping`` must be the name of the form
   template you want to use.
#. Line 2: Declare a ``Model`` object to hold data that needs to be passed to
   the template.
#. The method code performs any data manipulation required before rendering the
   form. The ``model.addAttribute`` statements would be included here.
#. The ``return`` string specifies the path to the template. Recall that Spring
   automatically adds MOST of the file path---up through ``.../templates``. You
   need to add any path details that follow.

   a. For example, if our ``templates`` folder contains a subfolder called
      ``events`` that holds a template called ``create.html``, then line 6
      would be ``return "events/create";``.

Add a Form Handler Method
--------------------------

Now that you have created and rendered a form in your ``coding-events``
project, you need to add a method to the controller to *handle* its submission.
Code along with the video below to add this functionality.

.. raw:: html

   <div style="text-align:center;">
      <iframe width="800" height="450" src="https://www.youtube.com/embed/LnpJcq33uoM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
   </div>

As usual, the following summary outlines the ideas from the clip.

Handle Form Submission
^^^^^^^^^^^^^^^^^^^^^^^

To *process* a form after the user clicks the *Submit* button, you need to add
a method to the controller using the ``@PostMapping`` annotation:

.. sourcecode:: java
   :linenos:

   @PostMapping("formTemplateName")
   public String processFormMethodName(@RequestParam Type parameter1, Type parameter2, ...) {

      // Method code...

      return "redirect:templateName";
   }

Some points to note:

#. Line 1: The string parameter for ``PostMapping`` must be the name of the
   form template.
#. Line 2: For each piece of data that needs to be retrieved from the form,
   declare a parameter of the appropriate type.

   .. admonition:: Note

      ``@RequestParam`` matches the parameters to the submitted data. For this
      to work, the parameter names MUST match the ``name`` attributes used in
      each of the ``input`` elements.

#. The method code performs any data manipulation required after the
   information gets submitted.
#. Line 6: Generally, we want to send the user to a different page after they
   successfully submit a form. Instead of re-rendering the form, the ``return``
   string *redirects* the user to a method that handles a different template.

Resources
----------

#. Coding events `starter code <https://github.com/LaunchCodeEducation/coding-events/tree/starter>`__.
