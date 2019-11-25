Static Resources
=================

Up to now, we used templates to display data sent by the controller as text in
the view. If we need to display an image or video, or if we want to create a
link to a different file, then we need to move beyond a text output.

With Thymeleaf, we can set values for the HTML ``src`` and ``href`` attributes.
Instead of hard-coding a file path or external URL inside a tag, ``th:src`` and
``th:href`` take advantage of a simpler ``@{filePath}`` syntax.

Accessing Resources
--------------------

Inside the ``resources`` folder, there is another directory called ``static``.
This is the location where we can store files that our project needs to
access---like images, CSS stylesheets, or JavaScript scripts.

``th:src``
^^^^^^^^^^^

Lorem ipsum...

``th:href``
^^^^^^^^^^^^

Lorem ipsum...

Check Your Understanding
-------------------------

Questions go here...
