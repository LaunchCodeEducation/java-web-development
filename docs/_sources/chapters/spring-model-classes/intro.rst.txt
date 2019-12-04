Old Content Notes
==================

Part 1 video here:
`Spring Boot Models, part 1 <https://education.launchcode.org/skills-back-end-java/videos/intro-to-spring-boot-models-1/>`__

Part 2 video here:
`Spring Boot Models, part 2 <https://education.launchcode.org/skills-back-end-java/videos/intro-to-spring-boot-models-2/>`__

Part 1 Notes
-------------

In this lesson we will focus on creating distinct, **POJO** model
objects. POJO stands for “plain, old Java object”. We will then move all
data operations out of the controller layer and into the model layer. We
will use model binding to auto-create model classes on form submission.

Code along with the video using the starter code below. There have been
some changes to the codebase since the last video, so you’ll want to
look at the branch listed below to get those changes.

Some Bootstrap classes we have added to improve the look and feel of our
application are: ``container``, ``form-group``, and ``form-control``.

If you haven’t already done this in the course of previous class
exercises, begin **refactoring** (*improving your code while not adding
new features*) your ``CheeseController`` by creating a ``models``
package and creating a ``Cheese`` Java class. Use auto-generation (see
Intelli-J Tip below) to create a constructor and the relevant getters
and setters. Continue refactoring ``CheeseController`` and then update
your templates to use the newly-created ``Cheese`` class instead.

At the end of this lesson, the remove functionality will not work. We
will tackle the solution to that problem, as well as how to get the data
out of our controller, in the next lesson!

Intelli-J Tip
~~~~~~~~~~~~~

Use right-click and select “Generate” to select among boilerplate code
generation options to speed up your program development.

Code
----

We start this lesson with the code in the ``video-models-pt1-start``
branch of the cheese-mvc repo: `starting
code <https://github.com/LaunchCodeEducation/cheese-mvc/tree/video-models-pt1-start>`__

We end this lesson with the code in the ``video-models-pt1-end`` branch
of the cheese-mvc repo: `ending
code <https://github.com/LaunchCodeEducation/cheese-mvc/tree/video-models-pt1-end>`__

References
----------

-  `Bootstrap <http://getbootstrap.com/>`__
-  `Bootstrap CDN <https://www.bootstrapcdn.com/>`__

Part 2 Notes
-------------

We’ll begin this lesson by designing a “remove” implementation that will
work with our new ``Cheese`` class. The first step is to create a field,
``cheeseId`` that will help us easily distinguish ``Cheese`` objects
that have the same name. Then we’ll create a “no-arg” constructor to
initialize this field and to increment the related static field,
``nextId``.

The controller should not be responsible for managing model objects in
any way at all. So let’s refactor ``CheeseController`` to move the data
management code into the ``CheeseData`` model class. Create the utility
methods ``getAll``, ``add``, ``remove``, and ``getById`` in that new
class. Now we can refactor ``CheeseController`` to use these methods. We
then need to modify our ``remove.html`` template to finish implementing
our “remove” functionality.

Next, we’ll refactor ``processAddCheeseForm`` and ``add.html`` to use
model binding. Model binding reduces the amount of code we need to write
and helps with validation (which we’ll explore further in a future
lesson). Because we use the ``@ModelAttribute`` annotation, Spring Boot
will try to create a ``Cheese`` object for us when it gets the ``POST``
request from ``/add``.

Code
----

We start this lesson with the code in the ``video-models-pt2-start``
branch of the ``cheese-mvc`` repo: `starting
code <https://github.com/LaunchCodeEducation/cheese-mvc/tree/video-models-pt2-start>`__

We end this lesson with the code in the ``video-models-part2-end``
branch of the ``cheese-mvc`` repo: `ending
code <https://github.com/LaunchCodeEducation/cheese-mvc/tree/video-models-part2-end>`__
