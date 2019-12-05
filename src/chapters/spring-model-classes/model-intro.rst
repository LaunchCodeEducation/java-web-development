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
#. The *model* is the data. Full stop.
#. The *controller* directs the flow of information between the view and the
   model. It does not store the data or determine how to display it for the
   user. However, it can manipulate data retrieved from the model or the view.

.. admonition:: Tip

   Need further review? Check out `this article <https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488>`__.

Model vs. Controller
---------------------

One tricky part of using the MVC structure is deciding what code belongs in the
model and what belongs in the controller.

#. Controller:

   a. Processing requests from the user,
   b. Rendering a view,
   c. Sending data to a view,
   d. Requesting data,
   e. Manipulating data,
   f. ...

#. Model:

   a. Storing and retrieving data,
   b. Organizing data,
   c. SOP involving the data,
   d. ...

Controller = Please give me this info, please store this, please delete this,
please show this to the user, please change this.

Model = How to store the data, how to retrieve data, how to organize data, how
to manipulate data independent of controller and view actions.

Check Your Understanding
-------------------------

Lorem ipsum...
