Bootstrap - Video
-----------------

.. todo:: Add model video #1, adding bootstrap here...

Bootstrap - Text
----------------

You'll notice in this section, not only are we updating our ``coding-events`` application to use models, but we've also
added some Bootstrap styling. Bootstrap is a commonly-used style library. It allows users to quickly apply its CSS style rules 
with class selectors. Style updates can add features or improve the usability of an application are therefore not refactoring.

For example, Bootstrap, and other styling libraries for tha matter, use a standardized color scheme for items like clickable
buttons. As the implementer of the helper library, you can apply the ``btn btn-primary`` classes to a button on your page and 
Bootstrap works behind the CSS scenes to render a blue button with white text in a legible font. For more customization, you 
could also choose which color you want all of a the buttons labelled with ``btn-primary`` on your web page to be. 

Straight out of the box, Bootstrap helps developers to get their web apps well styled without needing to spend much time writing
custom CSS rules. The library also does some of the work of applying user-experience best-practices. The button class ``btn-danger``
for example, is defaulted to appear red, a color most associated with danger. 

Image of standard HTML buttons without CSS:

.. figure:: figures/htmlDefaultButtons.png
   :alt: Standard HTML buttons.

HTML buttons without styling.

Same buttons with Bootstrap:

.. figure:: figures/bootstrapButtonOptions.png
   :alt: Some simple Bootstrap buttons.

Buttons styled with Bootstrap.

Adding Bootstrap to ``coding-events``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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


In the video, the Bootstrap classes ``container``, ``form-group``, and
``form-control`` are used to improve the look and feel of the views.
bootstrap classes to highlight - container, table, form-group, form-control

Bootstrap Layout
^^^^^^^^^^^^^^^^

QA lot of what makes Bootstrap a powerfully helpful and time-saving UI framework is the layout logic it contains.
In brief, Bootstrap uses a grid system of elements labelled *containers* and *rows* that respond dynamically to the
state of a web page. The grid elements are given a size label. The size dictates when an item will shift or change 
how it is rendered. Broadly speaking, the grid system helps developers write applications that work well on screens
of various sizes. But once you play around with it, you'll find that the grid layout can help you write apps that 
respond to more than just changes in window size.

TODO: find a good container/row example.

`Containers <https://getbootstrap.com/docs/4.4/layout/overview/#containers>`__.

Add a ``class=container`` to the body tag in ``templates/index.html``. 

Bootstrap Tables
^^^^^^^^^^^^^^^^

Bootstrap gives us some table styling that we can use to display events in ``coding-events``. Some table styling is
customizable, so read around Bootstrap's site and explore adding different options to your table.

TODO: find a good table example.

`Containers <https://getbootstrap.com/docs/4.4/layout/overview/#containers>`__.


Bootstrap Forms
^^^^^^^^^^^^^^^

Bootstrap offers a number of classes meant to decorate form elements. ``form-group`` helps classify items within
a form. ``form-control`` does something else I don't remember yet. 

TODO: find a good form example. update the link with the form component

`Containers <https://getbootstrap.com/docs/4.4/layout/overview/#containers>`__.
