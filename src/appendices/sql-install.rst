Installing SQL
==============

.. index:: SQL

A couple of chapters in this book cover SQL.
Before we get started learning the ins and outs of the language, let's make sure we have everything properly installed!
For this class, we will be using MySQL version 8.0.18, the most current version.

Mac Users
---------

First, we need to install MySQL itself.
The `Community Server 8.0.18 download page <https://dev.mysql.com/downloads/mysql/>`_ has a dropdown menu for the operating system you need.
Make sure you have selected MacOS before clicking *Download*!
You want to download the version called "macOS 10.14 (x86, 64-bit), DMG Archive".

#. When MySQL is done downloading, double-click on the disk image to launch the installer.
#. Click through the windows to install MySQL and agree to the terms and conditions.
#. When you reach the configuration window, you may have to enter a password for the root user. Pick a good password that you can remember!

Now that we have MySQL installed, we want to use it!
You can use MySQL in the terminal, however, many don't actually like it.
When working with MySQL in the terminal, all commands are final and you can't use any fun tools to visualize the tables.
Sounds like we should use a desktop client at first!

Now we need to install MySQL Workbench! 

The `MySQL Workbench 8.0.18 download page <https://dev.mysql.com/downloads/workbench/>`_ has a dropdown menu for the operating system. Make sure MacOS is selected before downloading!

Once you have MySQL workbench installed, double-click on the disk image to launch the installer.
Agree to the terms and conditions and install.

Now, we can use MySQL workbench to access our databases and practice our commands!

Windows Users
-------------

Windows users have a MySQL Installer available and that is what we will be using to install MySQL!
The `Installer download page <https://dev.mysql.com/downloads/installer/>`_ has a couple options available.
You want to download the version called "Windows (x86, 32-bit), MSI Installer" that specifies it is the "(mysql-installer-community-8.0.18.0.msi)". This should also be the version that uses at least 400 MB.
Make sure you have selected the correct option before clicking *Download*!

#. When MySQL is done downloading, open the installer.
#. The installer will install MySQL server and related tools. Select *Developer Default* and proceed!
#. The installer will check that the installs are compatible and install each one in turn. This may take a while so grab a snack!
#. When you reach the configuration window for MySQL server, you may have to enter a password for the root user. Pick a good password that you can remember!

The convenient thing about using the Windows installer is that our GUI client for the course is bundled in the install, so now we can open up MySQL Workbench.
MySQL Workbench will automatically scan for available MySQL servers. Yours should appear on the home screen. Double click and enter your password to get going!