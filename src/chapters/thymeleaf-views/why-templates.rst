Templates
==========

Take a look at the homepage for `WebElements <https://www.webelements.com/>`__.
The content includes text, images, a navigation bar, a search box, linked menu
options at the bottom of the page, and 118 carefully colored boxes with
links---one for each element on the periodic table. All of this content is
very deliberately arranged and styled.

Imagine your boss tasks you with creating this website. Setting up the
HTML tags for the navigation bar would be straightforward, but what about the
element boxes? You would need to make 118 similar structures, but with
different text, links, and colors. Trying to make the table structure work
would be tedious at best, and excruciatingly difficult at worst.

Also, what if a new element gets discovered, or some of the data for the
elements changes? Updating the text, colors, layout, etc. means adjusting those
items in the HTML. Also, if that information appears in other areas of the
website, then you need to modify that code as well.

Whew! Changing the website rapidly becomes problematic, especially since it
contains lots of data and consists of multiple pages. This is where templates
come in to play. They help automate the tasks required to build and maintain a
website.

Templates are Frameworks
-------------------------

.. index:: ! template

A **template** provides the general structure for a web page. Templates outline
for us and Spring where different elements get placed on the page. Any page
made with a template includes its elements and follows its rules. If we add
content to the template or modify it in some way, all pages made from that
template will reflect the changes.

Let's see how using a template makes our lives easier.

No Template
^^^^^^^^^^^^

The code below displays a simple list. It defines the location for the heading
and each ``<li>`` element, in addition to a couple of fun links. The CSS file
(not shown) specifies the font, text size, colors, etc.

.. sourcecode:: html
   :linenos:

   <body>
      <h1>Java Types</h1>
      <div class="coffeeList">
         <ol>
            <li>French Roast</li>
            <li>Espresso</li>
            <li>Kopi Luwak</li>
            <li>Instant</li>
         </ol>
      </div>
      <hr>
      <div class="links">
         <h2>Links</h2>
         <a href="https://www.launchcode.org/">LaunchCode</a> <br>
         <a href="https://en.wikipedia.org/wiki/Coffee">Coffee</a>
      </div>
   </body>

We could drastically improve the appearance and content of the page by playing
around with the tags, classes, styles and text. However, any change we want to
make needs to be coded directly into the HTML and CSS files, and this quickly
becomes inefficient.

A Better Way
^^^^^^^^^^^^^

Recall that a template represents a *view* in the MVC world. It sets up a
structure to display the data delivered by the controller, and the template
guides where that information goes. This provides much more flexibility than
hard-coding, since data can change based on a user's actions.

.. sourcecode:: guess
   :linenos:

   <body>
      <h1 {templateInstructions}></h1>
      <div class="coffeeList">
         <ul>
            <li {templateInstructions}></li>
         </ul>
      </div>
      <hr>
      <div class="links">
         <h2>Links</h2>
         <a {templateInstructions}></a>
      </div>
   </body>

This HTML looks similar to the previous example, but it replaces some of the
code with *instructions*.

``{templateInstructions}`` refers to instructions and data passed into the
template by the controller. These will automatically create HTML tags in order
to display or update the information.

By using a template to build the website, changing the list involves altering
something as simple as an ArrayList or object. After changing that data, the
template does the tedious work of modifying the HTML.

Templates Support Dynamic Content
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Besides making it easier to organize and display content, templates also allow
us to create a *dynamic* page. This means that its appearance changes to fit
new information. For example, we can define a grid for displaying photos in
rows of 4 across the page. Whether the images are of giraffes, tractors, or
balloons does not matter. The template sets the layout, and the code feeds in
the data. If more photos are found, extra rows are produced on the page, but
each row shows 4 images.

In the last lesson, you built a simple website that displayed a welcome message
and responded to changing values for a user's name. You did NOT apply a
template for this page, and it is possible to create an interactive site
without one. However, as your projects grow in size, templates make it MUCH
easier to maintain your work.

.. admonition:: Tip

   Use templates when building a web-based project.

Templates Provide Structure, Not Content
-----------------------------------------

Templates allow us to decide how to display data in the view, even if we do
not know exactly what that data will be. Information pulled from forms,
APIs, or user input will be formatted to fit within our design.

.. figure:: ./figures/ThymeleafTemplateDiagram.png
   :alt: Templates define where data gets displayed on a webpage.

In the figure, the black outlines represent different areas defined by the
template---spaces for lists, images, links, etc. As the controller feeds data
into the template, the appearance of the page changes.

.. admonition:: Note

   If the template expects data for a list, but the controller does not provide
   the information, that part of the screen remains empty.

Check Your Understanding
-------------------------

.. admonition:: Question

   Why should we use a template to design a web page rather than just coding
   the entire site with HTML and CSS?
