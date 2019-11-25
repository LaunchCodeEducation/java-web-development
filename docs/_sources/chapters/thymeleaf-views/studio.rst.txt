Studio: Spa Day!
================

After all of the hard work we have put into learning about Thymeleaf, it is
time for a spa day!
First, we need to put our knowledge of Thymeleaf to the test.
Instead of heading out to our favorite spa, let's make an application for the
owners!

Our application needs to do the following:

#. Display the user's name and skin type under their customer profile.
#. Display the appropriate facial treatments for their skin type.
#. Display the description of the spa's manicures or pedicures depending on the
   user's interest.

As always, read through the whole page before starting to code.

Setup
-----

Fork and clone the appropriate `repository <https://github.com/LaunchCodeEducation/spa-day-starter-code>`_. Check out the project via Version Control in IntelliJ.

When you open the project and run it using ``bootRun``, go to
``localhost:8080`` and you should see a form!

.. figure:: figures/startingform.png
   :alt: Image showing an empty form with three fields for name, skin type, and whether the person wants a pedicure or manicure.

The Customer Profile
--------------------

In ``controllers``, we have one controller called ``SpaDayController``. Inside
``SpaDayController``, we have three methods.

#. The ``checkSkinType()`` method. The owners gave us this method to help us
   figure out which facial treatments are appropriate for which skin type.
#. The ``customerForm()`` method, which looks very similar to what we did in
   the last lesson.
#. The ``spaMenu()`` method, which we will use to bring in our Thymeleaf
   template, ``menu.html``.

In ``templates``, we have a Thymeleaf template called ``menu.html``.
Inside ``menu.html``, there are two main divs in the body.
Let's focus on the div with the id, ``clientProfile``.

#. Add an ``h2`` that says "My profile".
#. Add a ``p`` tag and use ``th:text`` to bring in the value of ``name``.
#. Add a ``p`` tag and use ``th:text`` to bring in the value of ``skintype``.
#. Add a ``p`` tag and use ``th:text`` to bring in the value of ``manipedi``.

Run the application and head to ``localhost:8080`` to see the results! When we
fill out the form, we should see a new page with the client profile at the top!

List All Appropriate Facial Treatments
--------------------------------------

Luckily for us, the spa owners gave us the ``checkSkinType()`` method in our
``SpaDayController``. Also, our teammates already set up code in our
``spaMenu()`` method to fill an ``ArrayList<String>`` with facial treatments
that would work for the user's skin type. Now, we just need to use Thymeleaf to
display the appropriate facial treatments (stored in the ArrayList,
``appropriateFacials``)!

Let's head back to ``menu.html`` and checkout the empty div with the id,
``servicesMenu``.

Add a table and iteratively (using our ``th:block`` and ``th:each`` combo) add
rows for the values in ``appropriateFacials``. If you need a quick reminder of
the syntax, review the :ref:`th:block section <th-block>` .

Mani or Pedi?
-------------

One other thing the spa owners want to be cautious of is their treatment
descriptions. Because the descriptions rarely change and are going to be used
in multiple places on the site, the owners have written up the descriptions as
Thymeleaf fragments.

Checkout the file, ``fragments.html``, in the ``templates`` directory. The
owners have already written up the descriptions for their manicure and pedicure
in separate ``p`` tags.

We want to put the description in a ``div`` along with an ``h3`` stating that
it is either a manicure or pedicure. This new ``div`` should be inside the
``servicesMenu`` div.

Use ``th:if`` to determine if the value of ``manipedi`` is a ``"manicure"`` or
``"pedicure"``.

#. If the value of ``manipedi`` is ``"manicure"``, the ``div`` element
   containing the ``h3`` that says ``"Manicure"`` needs to be on the page and
   the ``p`` tag needs to be *replaced* with the fragment of the manicure
   description from ``fragments.html``.
#. If the value of ``manipedi`` is ``"pedicure"``, the ``div`` element
   containing the ``h3`` that says ``"Pedicure"`` needs to be on the page and
   the ``p`` tag needs to be *replaced* with the fragment of the pedicure
   description from ``fragments.html``.

End Result
----------

After you are done with the studio, you should be able to fill out the form,
click "Submit", and see your profile page.

.. figure:: figures/completedform.png
   :alt: Form completed with the name, "Yolanda", combination skin and a preference for pedicures.

.. figure:: figures/endresultprofilepage.png
   :alt: Profile showing Yolanda's information, recommended facial treatments, and pedicure description.

Bonus Mission
-------------

#. Modify ``styles.css`` to get some CSS practice! Try add a footer with square
   shaped ``div`` elements. Each square should be a different color for
   different available nail polishes.
#. Modify the form to allow the user to select either a manicure or pedicure or
   *both*. If the user selects both, display both the manicure and pedicure
   descriptions on the ``Spa Menu`` page.
#. Work with routes and paths to display the spa menu page on a separate route
   from the form.
