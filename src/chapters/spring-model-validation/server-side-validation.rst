Server-Side Validation
======================

.. index:: ! validation

Web applications work under the client-server model. We have been focusing on the server portion, using Spring Boot and Java to create server-side application code. A critical component of any well-made web application is **validation**, which is the process of checking that data conforms to certain criteria. Validation ensures that the application only stores meaningful data. 

.. _validation-example:

.. admonition:: Example

   Consider a user registration form on a web site. Effective validation rules might require that:

   - The username is between 3 and 12 characters long, and 
   - The password is at least 6 characters long.

.. index:: 
   single: validation, server-side
   single: validation, client-side

Web applications should validate *all* data submitted by users. This ensures that data remains well-structured and unexpected errors don't occur. Validation that occurs in the browser---using JavaScript or HTML attributes---is **client-side validation**. Validation that occurs on the web server is **server-side validation**. 

Even if client-side validation is done, it is still critical to validate data on the server. This is because client-side validation can often be bypassed by a savvy user. For example, such a user might modify HTML using a browser's developer tools, or disable JavaScript. 

Server-side validation involves both the model and controller. The model is responsible for *defining* validation rules, while the controller is responsible for *checking* validation rules when data is submitted to the server. 

Check Your Understanding
------------------------

.. admonition:: Question

   The best practice for validating data in a web app is to:

   #. Use client-side validation
   #. Use server-side validation
   #. Use both client-side and server-side validation
   #. Don't validate incoming data

.. ans: c, Use both client-side and server-side validation
