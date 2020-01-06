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

Windows users have a MySQL Installer available and that is what you will be using to install MySQL!
The `Installer download page <https://dev.mysql.com/downloads/installer/>`_ has a couple options available.
You want to download the version called ``"Windows (x86, 32-bit), MSI Installer"`` that specifies it is the ``"(mysql-installer-community-8.0.18.0.msi)"``.
This should also be the version that uses at least 400 MB (not the *web-community* version).
Make sure you have selected the correct option before clicking *Download*!

#. When MySQL is done downloading, open the installer.
#. The installer will install MySQL server and related tools. Select *Developer Default* and proceed.

   .. admonition:: Note

      If you receive a message on the *Check Requirements* page for any MySQL products or tools other than MySQL Workbench, you
      can safely ignore these and continue with *Next*.

      With the exception of creating and entering a password, you can move forward with the default selections to install and configure.


#. The installer will check that the installs are compatible and install each one in turn. This may take a while so grab a snack!
#. When you reach the configuration window for MySQL server, you may have to enter a password for the root user. Pick a good password that you can remember.

   .. admonition:: Warning

      Once you create a password for the root user, you cannot change it! Be careful when typing out the password.


The convenient thing about using the Windows installer is that our GUI client for the course is bundled in the install, so now you can open up MySQL Workbench
from the final page in the installation process. MySQL Workbench will automatically scan for available MySQL servers. Your local server
should appear on the home screen. Double click and enter your password to get going!
