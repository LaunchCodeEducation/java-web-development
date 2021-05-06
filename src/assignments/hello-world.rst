.. _assignment0:

Assignment #0: Hello, World!
============================

The purpose of this initial assignment is to familiarize yourself with the process of running the autograding tests and submitting your work via GitHub Classroom. Even if you are familiar with GitHub Classroom, this assignment will contain several new items that are specific to working with Java assignments.

Getting Started
---------------

Let's set up the assignment on our computer and learn about its basic structure.

First, find Assignment #0 in Canvas and click on the invitation link. After accepting, go to your assignment repository on GitHub.

Make sure IntelliJ is running and all project windows are closed. You should see IntelliJ's **Welcome** pane. From here, select the *Get from Version Control* option.

.. figure:: figures/check-out-from-vcs.png
   :alt: Select the Check Out From Version Control option

   IntelliJ Welcome Pane

While IntelliJ is working, go to your assignment repository on GitHub and copy the clone URL.

.. figure:: figures/copy-clone-url.png
   :alt: Click the Copy button in the Code dropdown

   Copying the repository's clone URL

Paste this URL in the URL field of the *Get from Version Control* pane that IntelliJ has opened. Make sure the *Directory* field is the location that you want your assignment to be saved within, then click the *Clone* button.

.. figure:: figures/url-field.png
   :alt: Paste the clone URL in IntelliJ's URL field

   The Clone URL field

After IntelliJ clones your repository, it will prompt you to open it. Select *Yes*.

.. figure:: figures/open-intellij-project.png
   :alt: IntelliJ asks whether or not you want to open the project after cloning

   Select Yes to open the newly cloned project

When the project opens initially, the *Project* pane, which shows the files within your project, may be closed. If so, click on the pane's button at the top left to open it.

.. figure:: figures/project-pane-closed.png
   :alt: The IntelliJ project with closed project pane

   The Project pane may be closed initially

Navigate though the directories down to the ``HelloWorld`` class. This will be in the ``src/main/java/`` directory. For all of the assignments we work on in this unit, our source code will live within this directory.

.. figure:: figures/hw-class.png
   :alt: The HelloWorld class file

   Navigate to the HelloWorld class and open it

Note that there are two green "play" buttons on the left of the source code. This indicates that IntelliJ recognizes this class as being runnable. You can use either of these buttons to run the program. They function exactly the same. Clicking on one of them opens up a menu with a few options. Choose the first to run the program.

.. figure:: figures/run-program.png
   :alt: Running the main program

   The Run Program menu

When the program runs, IntelliJ will open a pane at the bottom of the window and display program output. Currently, the program has no output. You'll fix that in a bit.

Running the Autograding Script
------------------------------

Up to now, you have have had to push your code to GitHub in order to see grading results. For this unit, you'll be able to run the autograding tests yourself *before* you push your code. This will make it quicker and easier to know whether or not your code is correct. Let's learn how to run the tests.

In the *Project* pane, navigate to the test class, ``TestHelloWorld``, in the directory ``src/test/java``. For each assignment, this directory will contain all of the autograding tests, and it may have more than one class.

.. figure:: figures/run-test-buttons.png
   :alt: Two green play buttons inside the test file

   Navigate to the TestHelloWorld class and open it

Notice the two slightly different "play" buttons at the left. The topmost button is actually two green "play" arrows staked on top of each other. It allows you to run *all* of the tests in a given file. 

The lower button, next to the ``testSayHello`` method, will run only that individual test. A test is a single method in a test file that has ``@Test`` just above it. A test file may have multiple tests.

Run all of the tests (in this case, there is only one) but clicking on the topmost button.

.. figure:: figures/run-all-tests.png
   :alt: The double play icon runs all tests in the file

   Running all tests in the file

A menu opens, and selecting the first option runs the tests.

.. figure:: figures/test-results-fail.png
   :alt: Test failure results

   The test initially fails

When IntelliJ runs the tests, it opens a pane at the bottom of the window to display test results. At the left, we see that the test has failed. We can expand the tree to see each of the individual tests (again, in this case there is only one). Selecting one of the tests shows its results to the right. 

This console-based test output can be hard to read, but IntelliJ provides a nicer interface for viewing test results. Follow the *Click to see difference* link to open this pane.

.. figure:: figures/test-results-comparison.png
   :alt: IntelliJ's results comparison screen

   Viewing expected versus actual results

On the left, you'll see the output that the test expected. On the right, you'll see the output that your program actually provided. IntelliJ will highlight the difference between the two, showing you exactly why your test failed.

In this case, the test expected our code to output ``Hello, World!``. Instead, it provided no output at all.

.. admonition:: Warning

   The autograding tests are VERY exacting. A difference of just one character will result in a failed test. The tests are also case-sensitive. You'll need to pay attention to detail in order complete your assignments.

When your code is correct, IntelliJ will display a green checkmark indicating passing tests.

.. figure:: figures/test-results-passing.png
   :alt: When you complete the assignment successfully all tests pass

   Passing test results

Your Task
---------

Your task is simple: make the program print out the string ``"Hello, World!"``. Edit the code in the ``HelloWorld`` class, withing the ``sayHello`` method. When your code is correct, running the tests will display passing results.

.. _submitting-your-work:

Submitting Your Work
--------------------

Once you get all of the tests to pass, open IntelliJ's *Terminal* pane. Then you should commit and push your code to GitHub.

.. figure:: figures/commit-and-push.png
   :alt: Git commands to commit and push code inside the Terminal pane

   Commit and push your code from within IntelliJ's Terminal pane

Visit your assignment repository page. Near the top right, you'll see a green checkmark indicating that GitHub has graded your assignment as passing. If you see a red X, then your assignment is not yet correct.

.. figure:: figures/green-checkmark.png
   :alt: A green checkmark next to the most recent commit ID

   A green checkmark shows that GitHub marked our assignment as passing

This process will be the same for all of your assignments in this unit. Revisit this page as needed to review instructions on running tests in Java projects.