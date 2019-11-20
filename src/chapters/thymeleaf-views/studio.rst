Studio: Spa Day!
================

After all of the hard work we have put into learning about Thymeleaf, it is time for a spa day!
However, first, we need to put our knowledge of Thymeleaf to the test.
Instead of heading out to our favorite spa, let's make an application for the owners!

Our application needs to do the following:

#. Display the user's name and skin type under their customer profile.
#. Display the appropriate facial treatments for their skin type.
#. Display the description of the spa's manicures or pedicures depending on the user's interest.

As always, read through the whole page before starting to code.

Setup
-----

Fork and clone the appropriate repository. Check out the project via Version Control in IntelliJ.

The Customer Profile
--------------------

In ``controllers``, we have one controller called ``SpaDayController``. Inside ``SpaDayController``, we have three methods.

#. The ``customerForm()`` method, which looks very similar to what we did in the last lesson.
#. The ``checkSkinType()`` method. The owners gave us this method to help us figure out which facial treatments are appropriate for which skin type.
#. The ``spaMenu()`` method, which we will use to bring in our Thymeleaf template, ``menu.html``.

In ``templates``, we have a Thymeleaf template called ``menu.html``.
Inside ``menu.html``, there are two main divs in the body.
Let's focus on the div with the id, ``clientProfile``.

#. Add an ``h2`` that says "My profile".
#. Add a ``p`` and using ``th:text``, bring in the value of ``name``.
#. Add a ``p`` and using ``th:text``, bring in the value of ``skintype``.
#. Add a ``p`` and using ``th:text``, bring in the value of ``manipedi``.

Run the application and head to ``localhost:8080`` to see! Now we should see the form and when we fill it out, we should see a new page with the client profile at the top!

List All Appropriate Facial Treatments
--------------------------------------

Luckily for us, the spa owners gave us the ``checkSkinType()`` method in our ``SpaDayController`` and our teammates already set up code in our ``spaMenu()`` method to fill an ``ArrayList<String>`` with facial treatments that would work for the user's skin type.
Now, we just need to use Thymeleaf to display the appropriate facial treatments (stored in the ArrayList, ``appropriateFacials``)!

Let's head back to ``menu.html`` and checkout the empty div with the id, ``servicesMenu``.

Add a table and iteratively (using our ``th:each`` and ``th:block`` combo) add rows for the values in appropriateFacials.

Mani or Pedi?
-------------

One other thing the spa owners want to be cautious of is their treatment descriptions.
Because the descriptions rarely change and are going to be used in multiple places on the site, the owners have written up the descriptions as Thymeleaf fragments.

Checkout the file, ``fragments.html``, in the ``templates`` directory.
The owners have already written up the decription for their manicure in a ``p`` tag and the description for their pedicure in a ``p`` tag.

We want to put the description in a div along with an ``h3`` stating that it is either a manicure or pedicure.

Use ``th:if`` to determine if the value of ``manipedi`` is a ``"manicure"`` or ``"pedicure"``. 
If the value of ``manipedi`` is ``"manicure"``, the ``div`` element containing the ``h3`` that says ``"Manicure"`` needs to be on the page and the ``p`` tag needs to be *replaced* with the fragment of the manicure description from ``fragments.html``.
If the value of ``manipedi`` is ``"pedicure"``, the ``div`` element containing the ``h3`` that says ``"Pedicure"`` needs to be on the page and the ``p`` tag needs to be *replaced* with the fragment of the pedicure description from ``fragments.html``.

Bonus Mission
-------------

#. Modify ``styles.css`` to get some CSS practice!
#. Modify the form to allow the user to select either a manicure or pedicure or *both*. If the user selects both, display both the manicure and pedicure descriptions on the ``Spa Menu`` page.
#. Work with routes and paths to display the spa menu page on a separate route from the form.