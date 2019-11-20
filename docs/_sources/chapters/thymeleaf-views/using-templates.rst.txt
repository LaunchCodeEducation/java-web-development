Using a Template
=================

The video on this page provides you some live-coding practice with Thymeleaf
templates. Be sure to code along as you watch the clip.

.. admonition:: Warning

   This video and the others in the chapter walk you through building a small
   web-based project. DO NOT SKIP this practice, because the end of chapter
   exercises pick up where the tutorials end.

Let's Get Started!
-------------------

   Video goes here...

Now that your project is started, let's review one skill and two
best-practices.

Passing Data to a Template
---------------------------

Discuss how to use an instance of the ``Model`` class to collect data in the
controller file into variables that can be accessed by the view (templates).

Discuss how to access data passed in by the controller using the ``${}``
syntax.

The data in single-value variables like ``title`` can be displayed as text
on the screen by using ``th:text = "${title}"``. This allows a webpage to
*dynamically* display data within an HTML element...

Setting Default Text
^^^^^^^^^^^^^^^^^^^^^

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
animal or function of the site. A better approach would be to divide the
templates into related categories like ``feedingSchedules``, ``concessions``,
``donations``, ``pachyderms``, etc. In turn, each of the subfolders can hold
finer categories as needed.

The goal is to consolidate your files into related groups. That way, you only
need to use a single file path in a given controller. This improves the
efficiency of your code, saves you from getting a headache trying to find and
fix a specific file, and streamlines updates by reducing the lines of code
that need to be modified.

Check Your Understanding
-------------------------

Questions go here...
