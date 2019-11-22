Using a Template
=================

The video on this page provides you some more live-coding practice with
Thymeleaf templates. Return to your ``hello-spring`` project and code along as
you watch the clip.

.. admonition:: Warning

   This video and the others in the chapter walk you through building a small
   web-based project. DO NOT SKIP this practice, because the end of chapter
   exercises pick up where the tutorials end.

Try It!
--------

   Video goes here...

Now that your project is growing, let's review one skill and two
best-practices.

Passing Data to a Template
---------------------------

The controller class contains methods that send data to different templates.
These methods have a structure similar to:

.. sourcecode:: Java
   :linenos:

   public String methodName(Model model) {

      // method code here

      model.addAttribute("variableName", variableValue);

      return "pathToTemplate";
   }

Each method that sends data to a template requires:

#. A ``Model`` parameter (line 1). This object stores the variable names and
   values that get passed into a template.
#. One or more ``addAttribute`` statements that add data to the ``model``
   object (line 5). ``variableName`` must be a string. ``variableValue`` can
   be a variable of any type, a number, a 'character', or a "string".
#. A ``return`` statement of type ``String``.
#. The ``return`` string contains the path and file name for the desired
   template (line 7). For example, if our ``templates`` folder contains a
   subfolder called ``animals`` and a template called ``dogs.html``, then the
   return statement would be ``return "animals/dogs";``.

Accessing Data in a Template
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Thymeleaf commands appear (in most cases) as *attributes* within a standard
HTML tag. Each keyword starts with the prefix ``th``.

.. sourcecode:: html

   <tag th:keyword = "..."></tag>

The code inside the quotation marks will vary depending on the keyword.
Usually, this will involve accessing data passed in from the controller.

The data available to a template includes any variables and values stored in
the ``model`` object, and this will be accessed with the syntax
``${variableName}``.

For example, in the video, we collected the value of the ``name`` variable
like so:

.. sourcecode:: html

   <p th:text = "${name}"></p>

The data in single-value variables like ``title`` can be displayed as text
on the screen by using ``th:text = "${title}"``. This allows a webpage to
*dynamically* display data within an HTML element...

Setting Default Text
---------------------

What if we want to view our template without running the program? As mentioned
earlier in the chapter, Thymeleaf files can be opened in a browser and
displayed as a webpage. With no data, however, opening a template shows blank
spaces wherever information from the controller is expected. Fortunately, we
can add some default text within the framework to give us an idea of what the
page will look like when we start the program.

To include default text in our template, simply include some *placeholder*
information inside the elements that contain a Thymeleaf attribute.

.. sourcecode:: HTML
   :linenos:

   <h2 th:text = "${title}">Default Title</h2>
   <div>
      <p th:text = "${bookQuote}">Don't Panic</p>
      <a th:text = "${linkText}">LaunchCode</a>
   </div>

The text ``Default Title``, ``Don't Panic``, and ``LaunchCode`` appear if we
open the template file in a browser. When the program runs, however, these text
samples will be replaced by the values stored in the ``title``, ``bookQuote``,
and ``linkText`` variables.

In most cases, you will never see the default text in our live webpage.
Including it helps, however, if you need to share the planned layout of the
webpage before the project is completely finished.

.. admonition:: Tip

   Best-practice encourages us to include default text in our templates. This
   improves the readability of the code, and it gives an outside observer a
   better idea of the structure of the webpage as well as of what data will
   appear in different sections.

Organizing Templates
---------------------

As any project grows, the number of templates required to build the website
will increase. Instead of just throwing all of the files into the
``templates`` folder, best-practice mandates that we place related items
into subfolders.

For example, if we build a website for a zoo, we can help ourselves immensely
by avoiding a ``templates`` folder with a single level of files for every
animal or feature of the site. A better approach would be to divide the
templates into related categories like ``feedingSchedules``, ``concessions``,
``donations``, ``pachyderms``, etc. Each subfolder can also hold finer
categories as needed.

The goal is to consolidate your files into related groups. That way, you only
need to use a single file path in a given controller. This improves the
efficiency of your code, saves you from getting a headache trying to find and
fix a specific file, and streamlines updates by reducing the lines of code
that need to be modified.

Check Your Understanding
-------------------------

Questions go here...
