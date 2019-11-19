Studio: Spa Day!
================

After all of the hard work we have put into learning about Thymeleaf, it is time for a spa day!
However, first, we need to put our knowledge of Thymeleaf to the test.
Instead of heading out to our favorite spa, let's make an application for the owners!

Our application needs to do the following:

#. Display the user's name and skin type under their customer profile.
#. Display the appropriate facial treatments for their skin type.

As always, read through the whole page before starting to code.

Setup
-----

Fork and clone the appropriate repository. Check out the project via Version Control.

The Customer Profile
--------------------

In ``controllers``, we have one controller called ``SpaDayController``. Inside ``SpaDayController``, we have three methods.

#. The ``customerForm()`` method, which looks very similar to what we did in the last lesson.
#. The ``checkSkinType()`` method. The owners gave us this method to help us figure out which facial treatments are appropriate for which skin type.
#. The ``spaMenu()`` method, which we will use to bring in our Thymeleaf template, ``menu.html``.

In ``templates``, we have one Thymeleaf template called ``menu.html``.
Inside ``menu.html``, there are two divs.
Let's focus on the div with the id, ``clientProfile``.

#. Add an ``h2`` that says "My profile".
#. Add a ``p`` and using ``th:text``, bring in the value of ``name``.
#. Add a ``p`` and using ``th:text``, bring in the value of ``skintype``.

Run the application and head to ``localhost:8080`` to see! Now we should see the form and when we fill it out, we should see a new page with the client profile at the top!

List All Appropriate Facial Treatments
--------------------------------------

Luckily for us, the spa owners gave us the ``checkSkinType()`` method in our ``SpaDayController`` and our teammates already set up code in our ``spaMenu()`` method to fill an ``ArrayList<String>`` with facial treatments that would work for the user's skin type.
Now, we just need to use Thymeleaf to display the appropriate facial treatments (stored in the ArrayList, ``appropriateFacials``)!

Let's head back to ``menu.html`` and checkout the empty div with the id, ``servicesMenu``.

Add a table and iteratively (using our ``th:each`` and ``th:block`` combo) add rows for the values in appropriateFacials.

Fragments
---------

Bonus Mission
-------------

#. Modify ``styles.css`` to get some CSS practice!
#. Work with routes and paths to display the spa menu page on a separate route from the form.
