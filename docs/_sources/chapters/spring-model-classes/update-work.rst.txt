Updating Past Work
===================

As you write more coding projects, at some point you will look back at
your early work and think, *Whoa! There is SUCH a better way to do that!* You
will spot places where your old code is inefficient, fragile, or contains a
bug.

This happens to all developers as our skills advance. We spot
places where our old code could be streamlined and strengthened.

.. admonition:: Examples

   Assume your past-self created a method to check if every integer in a single
   ArrayList is identical. Later, your more experienced self tackles the same
   problem.

   **Earlier self**:

   .. sourcecode:: Java
      :linenos:

      private static boolean checkIdentical(ArrayList<Integer> arr){
         int firstNum = arr.get(0);
         boolean identical = true;

         for (int num : arr){
            if (num != firstNum){
               identical = false;
            }
         }

         return identical;
      }

   This code compares the first number in the list to every other value. It
   works, but it's not very efficient.

   **Current self**:

   .. sourcecode:: Java
      :linenos:

      private static boolean checkIdentical(ArrayList<Integer> arr){

         return Collections.min(arr) == Collections.max(arr);

      }

   Bam! One line, no loop. You rock!

Refactoring Code
-----------------

Rather than feeling sheepish about the earliest code you generated, you can
always go back and make updates.

.. index:: refactor

**Refactoring** occurs when you improve your old work without adding any new
features. This process is not the same as debugging, since your old code runs
just fine. Instead, refactoring makes your code shorter, dry-er, more efficient, more
flexible, sturdier, or more legible.

We've mentioned refactoring several times before, and even have given you explicit instructions
to refactor with the Tech Jobs Assignments. We bring it up here to emphasize how commonplace the 
practice of refactoring is, not just in the context of learning, but always. 

Bootstrap
----------

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

Useful links to Bootstrap documentation:

#. `Components menu, buttons <https://getbootstrap.com/docs/4.0/components/buttons/>`__,
#. `Content menu, tables <https://getbootstrap.com/docs/4.0/content/tables/>`__.


Adding Generic Code
--------------------

.. index:: ! boilerplate code

From time to time, you will see the term **boilerplate code**. This refers to
generic, ready-made code that you can paste into just about any class or
template. Usually, you quickly modify this code to better fit your project,
but the boilerplate statements fill in some of the tedious structure and
routine commands. This saves you time and allows you to focus on the more
interesting parts of your work.

In the second :ref:`Classes and Objects chapter <equals-shortcut>` as well as
in :ref:`Assignment #2 <generator-shortcut>`, you used the IntelliJ *Generate*
shortcut to insert getters, setters, and custom methods into your Java classes.

The *Generate* shortcut can also be used to quickly format class constructors,
which is especially useful if you have declared many field variables.

.. figure:: figures/generateConstructorMenu.png
   :alt: Generate menu options.

Generate menu options.

Note that when you select *Generate --> Constructor*, you will be able to
select which fields to add to the constructor.

Adding a Default Constructor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Lorem ipsum...

Not sure if this section should go here or in the Apply Model Binding page.

Try It!
--------

Code along with the video below as you refactor your ``coding-events`` project.
You will add a model to deal with the event data, and you will revise the
templates to work with event objects.

.. todo:: Add model video #1 here...
