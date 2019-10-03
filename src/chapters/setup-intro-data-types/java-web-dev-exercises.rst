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

   .. note::

      If the app opens up to an existing project, select *IntelliJ >
      Preferences > Appearance & Behavior > System Settings* and un-check
      *Reopen last project on startup*. (For Windows users: *File >
      Settings > Appearance & Behavior > System Settings*.) Close and
      Reopen IntelliJ.

#. From the "Welcome to IntelliJ" dialog, select *Check out from Version
   Control > Git*

   .. figure:: figures/IntelliJVCS.png
      :scale: 40%
      :alt: IntelliJ VCS

      IntelliJ VCS

#. Click the button on the lower left corner of the dialog to log in to your
   Github account.

   .. figure:: figures/IntelliJGithub.png
      :scale: 65%
      :alt: IntelliJ Github

      IntelliJ Github

   .. note::

      To work with a remote repository in IntelliJ, you need to configure the
      program to access your GitHub account. We recommend authenticating your
      account using a token. This takes only one brief extra step, and will
      prevent you from having to update IntelliJ settings when you ever change
      your GitHub password.

#. From the URL dropdown options, select your fork of
   ``java-web-dev-exercises``, along with an appropriate source destination
   directory (i.e. a folder where you’ve stored other projects for this class).

   .. figure:: figures/IntelliJRepoSelection.png
      :scale: 80%
      :alt: IntelliJ Repo Selection

      IntelliJ Repo Selection

#. When asked "Would you like to create an IDEA project…" select *Yes*.

   .. figure:: figures/IntelliJAddFileToGit.png
      :scale: 40%
      :alt: IntelliJ Add File To Git

      IntelliJ Add File To Git

#. You'll then be presented with several pages that ask you about other
   settings for your project. Select the *Next* button on all of these pages,
   accepting the default settings.

#. When your project is ready, you'll see a page that looks like the image
   below. Click on the area in the top left labelled *Project*.

   .. figure:: figures/IntelliJNewProject.png
      :scale: 30%
      :alt: IntelliJ New Project

      IntelliJ New Project

#. Clicking on *Project* opens a side panel, displaying the file structure of
   the project you have just set up.

   .. figure:: figures/IntelliJProjectWindow.png
      :scale: 30%
      :alt: IntelliJ Project Window

      IntelliJ Project Window

#. Double-clicking on the *Hello* file opens the file to the right.

   .. figure:: figures/IntelliJOpenFile.png
      :scale: 35%
      :alt: IntelliJ Open File

      IntelliJ Open File

#. To run the *Hello* program, click on the green arrow next to the class
   definition and select *Run 'Hello.main()'* from the dropdown menu.

   .. figure:: figures/IntelliJRunFile.png
      :scale: 35%
      :alt: IntelliJ Run File

      IntelliJ Run File

   After a few seconds, you should see a new window appear with your program's
   output.

   .. figure:: figures/IntelliJFileOutput.png
      :scale: 35%
      :alt: IntelliJ File Output

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

