Bootstrap
=========

Introduction
------------

Bootstrap is a commonly-used style library. It allows users to quickly apply its CSS style rules 
with class selectors. Style updates can add features or improve the usability of an application. For example, 
Bootstrap, and other styling libraries for that matter, use a standardized color scheme for items like clickable
buttons. As the implementer of the helper library, you can apply the ``btn btn-primary`` classes to a button 
on your page and Bootstrap works behind the CSS scenes to render a blue button with white text in a legible 
font. For more customization, you could also choose which color you want all of a the buttons labelled with 
``btn-primary`` on your web page to be. 

Straight out of the box, Bootstrap helps developers to get their web apps well-styled without needing to spend 
much time writing custom CSS rules. The library also does some of the work of applying user-experience 
best-practices. The button class ``btn-danger`` for example, is defaulted to appear red, a color most 
associated with danger. 

Image of standard HTML buttons without CSS:

.. figure:: figures/htmlDefaultButtons.png
   :alt: Standard HTML buttons.

HTML buttons without styling.

Same buttons with Bootstrap:

.. figure:: figures/bootstrapButtonOptions.png
   :alt: Some simple Bootstrap buttons.

Buttons styled with Bootstrap.

Adding Bootstrap to ``coding-events``
-------------------------------------

Bootstrap - Video
^^^^^^^^^^^^^^^^^

.. youtube::
   :video_id: w-f3NYHHe9Q
   :gh_path: LaunchCodeEducation/coding-events/add-bootstrap

Apart from adding the library to your Spring Boot project, we won't focus much time on the individual 
Bootstrap updates to ``coding-events`` but we want you to know what they are and where they come from.
Feel free to add as much or as little Bootstrap styling to your own version.

.. index:: ! cdn, content delivery network

You'll see from the `Getting Started <https://getbootstrap.com/docs/4.0/getting-started/introduction/>`__ page 
that there are few ways to incorporate Bootstrap as a dependency in your project. One method is with a link to 
a **content delivery network**, or **CDN** for short. Linking to a CDN allows you to take advantage of the publicly
available library without downloading the entire codebase yourself. Think of the practice like using a web address 
of an image hosted somewhere else on the web. Unlike downloading the image and including it directly in your 
own repository, you are not the steward of the image's longevity. The path to an externally hosted image may 
get moved at some point, or even removed entirely. The same is true with CDNs. So when you use a dependency from 
a CDN, know that you may need to update the link at some point in your project's lifetime.

From `Bootstrap CDN <https://www.bootstrapcdn.com/>`__, copy the *Complete CSS* and *Complete JavaScript* addresses
and drop them into the head tag of ``fragments.html`` in your ``coding-events`` project.

.. sourcecode:: html
   :linenos:

   <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
   <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>

.. admonition:: Note

   The addresses you find at `Bootstrap CDN <https://www.bootstrapcdn.com/>`__ may be different from those 
   above.


Bootstrap Layout
^^^^^^^^^^^^^^^^

Much of what makes Bootstrap a powerfully helpful and time-saving style library is the layout logic it contains.
In brief, Bootstrap uses a grid system of elements labelled *containers* and *rows* that respond dynamically to the
state of a web page. Grid elements are given a size label that dictates when an item will shift or change 
how it is rendered. Broadly speaking, the grid system helps developers write applications that work well on screens
of various sizes. Once you play around with it, you'll find that the grid layout can help you write apps that 
respond to more than just changes in window size.


`Bootstrap Grid <https://getbootstrap.com/docs/4.4/layout/grid/>`__.


Bootstrap Tables
^^^^^^^^^^^^^^^^

Bootstrap gives us some table styling that we can use to display events in ``coding-events``. Some table styling is
customizable, so read around Bootstrap's site and explore adding different options to your table.


`Bootstrap Tables <https://getbootstrap.com/docs/4.4/content/tables/>`__.


Bootstrap Forms
^^^^^^^^^^^^^^^

Bootstrap offers a number of classes meant to decorate form elements. ``form-group`` helps organize items 
within a form so that inputs and corresponding labels stay visually connected. ``form-control`` can be applied 
to any type of form input to give it the Bootstrap style and look.


`Bootstrap Forms <https://getbootstrap.com/docs/4.4/components/forms/>`__.

Check Your Understanding
-------------------------

.. admonition:: Question

   True/False: Style updates are considered refactoring, since they add no new features to a project, only make it look better.

   #. True
   #. False

.. ans: false, style contributes to user interaction and experience and updates are therefore not refactoring
