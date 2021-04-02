Java Web Dev Exercises
======================

Initial Setup
-------------

The steps here will walk you through setting up a repository that you’ll
use to study example code, work on studios, and complete your first
assignment of this unit.

#. Create a *Fork* of `LaunchCodeEducation/java-web-dev-exercises <https://github.com/LaunchCodeEducation/java-web-dev-exercises>`__.
   Do not clone and create a local version of this repo just yet.

#. Open IntelliJ.

   .. admonition:: Note

      If the app opens up to an existing project, simply close that window to
      return to the welcome screen.
      
      If you prefer to have IntelliJ NOT open your most recent project, select
      *IntelliJ > Preferences > Appearance & Behavior > System Settings* and
      un-check *Reopen last project on startup*. (For Windows users: *File >
      Settings > Appearance & Behavior > System Settings*).

#. The *Welcome to IntelliJ* dialog looks different now. It includes a list of
   your most recent projects. However, we have the same three options in the
   upper-right corner. Select *Get from VCS*.

   .. figure:: figures/IntelliJVCS.png
      :alt: IntelliJ VCS button
      :width: 80%

      Clone a repository from a version control system.

#. Select the *GitHub* option on the left side of the next window. Click
   *Log In via GitHub* or *Use token* and follow the on-screen prompts.

   .. figure:: figures/IJ-github-login.png
      :alt: IntelliJ login to GitHub button

      Set up IntelliJ to talk to your GitHub account.

   .. admonition:: Note

      To work with a remote repository in IntelliJ, you need to configure the
      program to access your GitHub account. We recommend authenticating your
      account using a **token**. This takes only one brief extra step, and will
      prevent you from having to update IntelliJ settings whenever you change
      your GitHub password.

#. Now return to the *Repository URL* tab. From the URL dropdown options,
   select your fork of ``java-web-dev-exercises``, along with an appropriate
   source destination directory (like the folder where you’ve stored other
   projects for this class).

   When ready, click the *Clone* button!

   .. figure:: figures/IntelliJRepoSelection.png
      :alt: IntelliJ Repo Selection

      IntelliJ Repo Selection

#. If you're asked about other settings for your project. Select the *Next*
   button every time to accept the default options.
#. When your project is ready, you'll see a page that looks like the image
   below. Click on the area in the top left labelled *Project*.

   .. figure:: figures/IntelliJNewProject.png
      :alt: IntelliJ New Project
      :width: 80%

      IntelliJ New Project

#. Clicking on *Project* opens a side panel, displaying the file structure of
   the project you have just set up.

   .. figure:: figures/IntelliJProjectWindow.png
      :width: 80%
      :alt: IntelliJ Project Window

      IntelliJ Project Window

#. Double-clicking on the *Hello* file opens it in the workspace to the right.

   .. figure:: figures/IntelliJOpenFile.png
      :width: 80%
      :alt: IntelliJ Open File

      IntelliJ Open File

#. To run the *Hello* program, click on the green arrow next to the class
   definition and select *Run 'Hello.main()'* from the dropdown menu.

   .. figure:: figures/IntelliJRunFile.png
      :alt: IntelliJ Run File

      IntelliJ Run File

   After a few seconds, you should see a new window appear with your program's
   output.

   .. figure:: figures/IntelliJFileOutput.png
      :alt: IntelliJ File Output
      :width: 80%

      IntelliJ File Output

With that, you’re ready to go!

Troubleshooting
---------------

ClassNotFoundException
^^^^^^^^^^^^^^^^^^^^^^

If you experience ``java.lang.ClassNotFoundException`` when trying to
run code after setting up the project, follow these steps:

#. Select *File > Close Project*. If you have any other IntelliJ projects open,
   close them as well.

   .. figure:: figures/closeProject.png
      :scale: 40%
      :alt: Close Project

      Close Project

#. You should see the IntelliJ startup window, click the *X* next to
   ``java-web-dev-exercises`` in the left-hand pane.

   .. figure:: figures/startupWithProject.png
      :scale: 40%
      :alt: Startup with Project

      Startup with Project

#. From the same startup window, select *Import Project* from the right-hand
   pane.

   .. figure:: figures/startupWithoutProject.png
      :scale: 40%
      :alt: Startup without Project

      Startup without Project

#. Follow the steps that IntelliJ guides you through, accepting all defaults.
   When prompted to overwrite IntelliJ settings files, confirm that you want to
   do so.

