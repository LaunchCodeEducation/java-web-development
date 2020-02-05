Template Fragments
====================

Just like methods in Java provide us with the ability to reuse useful code,
Thymeleaf allows us to do something similar with HTML.

.. index:: ! fragments

**Fragments** are blocks of HTML elements that we want to use across multiple
templates. The fragments are stored in a separate file, and they can be
accessed by using the keywords ``fragment`` and ``replace``.

A summary of these two keywords is given below, followed by another
:ref:`video walkthrough <coding-events-fragments-vid>` to give you some more
live-coding practice.

Fragments DRY Your Code
------------------------

Anytime you find yourself typing identical code into different templates, you
should consider ways to streamline your work.

Never fear, coder. Fragments are the tool you need. The general syntax is:

.. sourcecode:: groovy

   th:fragment = "fragmentName"
   th:replace = "fileName :: fragmentName"

``th:fragment``
^^^^^^^^^^^^^^^^

Let's assume that you want to add the same styled header and a set of links to
multiple pages within your web project.

.. admonition:: Examples

   The common header styled with CSS:

   .. sourcecode:: HTML
      :linenos:

      <h1 class="fancyTitle" th:text="${title}></h1>

   The link list, which appears below a dividing line:

   .. sourcecode:: HTML
      :linenos:

      <hr>
      <a href = "https://www.launchcode.org">LaunchCode</a> <br/>
      <a href = "https://www.lego.com">Play Well</a> <br/>
      <a href = "https://www.webelements.com">Other Building Blocks</a>

Instead of pasting this code into every template, we will store the HTML in
a separate file.

#. Create a new html file inside the ``templates`` folder and give it a clear
   name (e.g. ``fragments.html`` is a common practice).
#. Inside this file, use the ``th:fragment`` attribute on each block of code
   that you want to reuse. Note that you must provide a different name for each
   sample.

   .. admonition:: Examples

      For the ``h1`` element:

      .. sourcecode:: HTML
         :linenos:

         <h1 th:fragment = "styledHeader" class="fancyTitle" th:text="${title}></h1>

      For multiple elements, we need to wrap them in another tag:

      .. sourcecode:: HTML
         :linenos:

         <div th:fragment = "linkList">
            <hr>
            <a href = "https://www.launchcode.org">LaunchCode</a> <br/>
            <a href = "https://www.lego.com">Play Well</a> <br/>
            <a href = "https://www.webelements.com">Other Building Blocks</a>
         </div>

We can now pull either of the fragments---``styledHeader`` or
``linkList``--into any template in our project.

.. admonition:: Tip

   What if we do not want to keep the link list inside its own ``div`` element?
   One option is to use ``th:block``:

   .. sourcecode:: HTML
      :linenos:

      <th:block th:fragment = "linkList">
         <hr>
         <a href = "https://www.launchcode.org">LaunchCode</a> <br/>
         <a href = "https://www.lego.com">Play Well</a> <br/>
         <a href = "https://www.webelements.com">Other Building Blocks</a>
      </th:block>

   Another option is to use the attribute ``th:remove``, which allows us to
   selectively discard the wrapper tag, but not any of its children.

   .. sourcecode:: html
      :linenos:

      <div th:fragment = "linkList" th:remove = "tag">

   For a more detailed discussion of the different ``th:remove`` options, consult
   the `Thymeleaf documentation <https://www.thymeleaf.org/doc/tutorials/2.1/usingthymeleaf.html#removing-template-fragments>`__.

``th:replace``
^^^^^^^^^^^^^^^

This attribute does just what the name implies---it *replaces* the tag that
contains it with the selected fragment. Thus, if the fragment is a ``<p>``
element, and the template contains ``<div th:replace = "...">``, then the
``div`` in the template will be replaced with a ``p``. Similarly, if the
fragment contains multiple elements, the single template tag will be replaced
with the entire code block.

Take home lesson: The template tag that contains ``th:replace`` does NOT have
to match the HTML tags in the fragment.

Now let's see how to pull fragments into a template:

.. admonition:: Examples

   .. sourcecode:: HTML
      :linenos:

      <!DOCTYPE html>
      <html lang="en" xmlns:th="http://www.thymeleaf.org/">
      <head th:fragment="head">
         <meta charset="UTF-8"/>
         <title th:text="${pageTitle}"></title>
      </head>
      <body>

         <h1 th:replace = "fragments :: styledHeader"></h1>

         <!-- Specific template code here... -->

         <p th:replace = "fragments :: linkList"></p>

      </body>

When the code runs, the ``h1`` element in line 9 will be replaced by the
``styledHeader`` fragment stored in the ``fragments.html`` file. Also, the
``p`` element in line 13 will be replaced by the ``<hr>`` and three ``<a>``
elements defined in the ``linkList`` fragment.

.. _coding-events-fragments-vid:

Try It!
--------

Code along with the following video to practice using fragments in your
templates:

.. youtube::
   :video_id: rbIyV6OoS-o

Remember that the summary text for the ``fragment`` and ``replace`` keywords
supports the video and is NOT intended as a replacement.

Check Your Understanding
-------------------------

.. admonition:: Question

   Given our code fragment in ``fragments.html``:

   .. sourcecode:: HTML
      :linenos:

      <th:block th:fragment = "linkList">
         <hr>
         <a href = "https://www.launchcode.org">LaunchCode</a> <br/>
         <a href = "https://www.lego.com">Play Well</a> <br/>
         <a href = "https://www.webelements.com">Other Building Blocks</a>
      </th:block>

   Which of the following would place the ``linkList`` fragment inside a
   ``<div>`` element in the template?

   #. ``<div th:replace = "fragments :: linkList"></div>``
   #. ``<div>${th:replace = "fragments :: linkList"}</div>``
   #. ``<div><p th:replace = "fragments :: linkList"></p></div>``
   #. ``<p><div th:replace = "fragments :: linkList"></div></p>``

.. Answer = c

.. admonition:: Bonus Question

   Research ``th:remove`` to answer this question. Which of the following does
   NOT remove the wrapper tag but does eliminate all of its children.

   #. ``th:remove = "all"``
   #. ``th:remove = "body"``
   #. ``th:remove = "tag"``
   #. ``th:remove = "all-but-first"``
   #. ``th:remove = "none"``

.. Answer = b
