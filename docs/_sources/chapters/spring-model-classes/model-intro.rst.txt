Models in MVC
==============

In the previous chapters, you learned about *views*, which display data and an
interface for a user, and *controllers* which determine what data to send the
the views. However, this data needs to come from some source.

We are now ready to take a closer look at the remaining part of the MVC
structure---models.

What is a Model?
-----------------

.. index:: model

A *model* represents a collection of data and the logic for accessing or
storing the data. That's it. This is what makes models a fabulous idea.
Properly constructed, they do NOT depend on any controllers or views, which
makes models easy to reuse without modification.

Consider a physical address book (a model). It stores names, addresses, phone
numbers, etc. on its pages. Anyone (a controller) can pick up the book,
retrieve the information, and then write some of the data on a separate piece
of paper (a view). The model itself does not depend on who picks it up or how
neatly the data gets printed on the scrap of paper. The book just provides
storage space and organization.

Quick Recap
^^^^^^^^^^^^

#. The *view* displays data in a way that the user can understand. It also
   provides options for the user to interact with the program (e.g. buttons or
   forms). The view communicates with the controller but not the model.
#. The *model* stores and maintains the data. Full stop.
#. The *controller* directs the flow of information between the view and the
   model. It does not store the data or determine how to display it for the
   user. However, it can manipulate data retrieved from the model or the view.

.. admonition:: Tip

   Need further review? Check out `this article <https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488>`__.

Model vs. Controller
---------------------

One tricky part of using the MVC structure is deciding what code belongs in the
model and what belongs in the controller. In general, any code that deals with
data transfer or responding to user actions belong in the controller. Code that
involves retrieving, storing, organizing, or maintaining data belongs with the
model.

Data manipulation can occur in either the model or controller, so we need to
make a distinction between these actions. For any manipulations that must occur
regardless of a user's actions, that code belongs in the model. For changes
that vary depending on a user's request (e.g. multiplying vs. adding a set of
numbers), that code belongs in the controller.

Model code defines the logic for processes that the user never needs to see.
These include:

#. The mechanics for storing data,
#. The mechanics for retrieving data,
#. The mechanics for organizing data,
#. Updating or manipulating the data independent of any controller or view
   actions.

Controller code handles *requests* made by the user. These include:

#. "Please retrieve this information from the model",
#. "Please store this in the model",
#. "Please delete this",
#. "Please change this",
#. "Please display this",
#. "Please modify this data in a novel way".

Note that a controller does not permanently store data. Instead, it sends the
information to the model, which uses its own code to preserve the data.

Check Your Understanding
-------------------------

Lorem ipsum...
