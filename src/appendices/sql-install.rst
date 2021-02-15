.. _sql-installation:

Installing SQL
==============

.. index:: SQL

A couple of chapters in this book cover SQL.
Before we get started learning the ins and outs of the language, let's make sure we have everything properly installed!
For this class, we will be using MySQL version 8.0.18, the most current version. Windows and Mac installations look a little different, so make sure you are following the appropriate directions for your machine.

.. admonition:: Note

   No matter your operating system, before you download any MySQL product, you are prompted to create an account.
   You do not have to do so if you do not want to! Below the buttons to log in, there is an option to skip creating an account and proceed with the download.


Mac Users
---------

First, you need to install MySQL itself.
The `Community Server 8.0.18 download page <https://dev.mysql.com/downloads/mysql/>`_ has a dropdown menu for the operating system you need.
Make sure you have selected MacOS before clicking *Download*!
You want to download the version called ``"macOS 10.14 (x86, 64-bit), DMG Archive"`` that specifies it is the ``"(mysql-8.0.18-macos10.14-x86_64.dmg)"``.
This option should also be at least 300 MB.

#. When MySQL is done downloading, double-click on the disk image to launch the installer.
#. Click through the windows to install MySQL and agree to the terms and conditions.
#. When you reach the configuration window, you may have to enter a password for the root user. Pick a good password that you can remember.

   .. admonition:: Warning

      Once you create a password for the root user, you cannot change it! Be careful when typing out the password.

Now that you have MySQL installed, you want to use it!
You can setup MySQL for use in the terminal, however, many don't actually like it.
When working with MySQL in the terminal, you can't use any fun tools to visualize the tables.
Sounds like you should use a desktop client at first to practice! For these reasons, we will be using MySQL Workbench as our GUI client to work with our databases.

The `MySQL Workbench 8.0.18 download page <https://dev.mysql.com/downloads/workbench/>`_ has a dropdown menu for the operating system. Make sure MacOS is selected before downloading.

.. admonition:: Warning

      If you are using a MacOS version prior to 10.14, use an older version of MySQL Workbench (6.3.10) by clicking the link that reads
      "Looking for previous GA versions?".

      This previous version is only compatible with a *legacy password encryption* option. If you did not select this when downloading MySQL
      (or you are not sure),

      #. Open MySQL from System Preferences and select *Initialize Database*.
      #. Enter your root user password choose the *Use Legacy Password Encryption* option.
      #. After hitting *OK*, start the MySQL Server again by clicking *Start MySQL Server*.

Once you have downloaded MySQL workbench, double-click on the disk image to launch the installer.
Agree to the terms and conditions and install.

Now, you can use MySQL workbench to access databases and practice commands!
When you first open MySQL workbench, you will see your local MySQL server on the homepage.
Double-click to access the server, enter the password, and you're ready to start querying away!

Windows Users
-------------

Windows users have a MySQL Installer available and that is what you will be
using to install MySQL! The `Installer download page <https://dev.mysql.com/downloads/installer/>`__
has a couple options available. You want to download the version called
``"Windows (x86, 32-bit), MSI Installer"`` that specifies the *community*
installer (not the *web-community* version). The download should require at
least 400 MB of space. Make sure you have selected the correct option before
clicking *Download*!

.. figure:: figures/sql-installer.png
   :alt: Select the community version of the installer program.
   :width: 70%

   The version number might be different, but the larger installation package is what you want.

.. admonition:: Note

   If you are prompted to sign up for a ``MySQL Community`` account, scroll to the
   bottom of the page and select ``No thanks``.

#. When MySQL is done downloading, open the installer.
#. The application will install MySQL server and related tools. Select
   *Developer Default* and proceed.

   .. figure:: figures/sql-install-1.png
      :alt: Select the Developer Default option in the first installation panel.
      :width: 80%

#. In the *Check Requirements* panel, ignore the options in the box and click
   *Execute*. With the exception of creating and entering a password, you can
   use the default selections to install and configure MySQL.

   .. figure:: figures/sql-install-2.png
      :alt: Click "Execute" instead of "Next" in the Check Requirements panel.
      :width: 80%

#. If the *Check Requirements* panel returns, you can simply click *Next*. You
   don't need to install Visual Studio, Python, or any of the other ``Manual``
   options.

   .. figure:: figures/sql-install-3.png
      :alt: Click "Next" if the Check Requirements panel returns.
      :width: 60%

#. The application will check that each component is compatible and install
   each one in turn. This may take a while, so grab a snack!

   .. figure:: figures/sql-install-4.png
      :alt: Click "Execute" to continue the installation.
      :width: 60%

#. When you reach the *Product Configuration* panel for MySQL server, click
   *Next*. All of the default options are fine.
   
   On the *Accounts and Roles* panel, enter a password for the root user. Pick
   a good one that you can remember.

   .. figure:: figures/sql-install-5.png
      :alt: Enter a password for the root user.

   .. admonition:: Warning

      Once you create a password for the root user, you cannot change it!

      If you forget your root user password, there is no easy option to reset
      it. You will need to uninstall MySQL, then repeat the installation
      process from the beginning.

#. The next panel is *Apply Configuration*. Just click *Execute*. This process
   will also take some time, so be patient. When it's done, click *Finish*.

   .. figure:: figures/sql-install-6.png
      :alt: Apply configurations, then click Finish.
      :width: 60%

      Almost done now!

#. The next series of panels configure a server on your machine. Accept all the
   default suggestions. Eventually, you will need to enter your root user
   password. Do this, then click *Check* and *Next*.

   .. figure:: figures/sql-install-7.png
      :alt: Enter root user password to connect to the server.
      :width: 60%

      Remember your root user password!

#. Continue clicking through the next several panels, accepting the default
   options as you go. Eventually, you will hit the final *Finish* button. Click
   it, and MySQL Workbench will be ready to launch!

   .. figure:: figures/sql-install-8.png
      :alt: Click Finish to launch MySQL.
      :width: 60%

      Ready to go.

The convenient thing about using the Windows installer is that our GUI client
for the course is bundled in the install, so now you can open up MySQL
Workbench from the final page in the installation process. MySQL Workbench will
automatically scan for available MySQL servers. Your local server should appear
on the home screen. Double click and enter your password to get going!
