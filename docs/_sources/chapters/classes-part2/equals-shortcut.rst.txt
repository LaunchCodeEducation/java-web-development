.. _equals-shortcut:

IntelliJ Generator Shortcut
============================

Instead of cutting, pasting, and refactoring old code to ensure that you create
a well-structured ``hashCode()`` method whenever you define your own
``equals()`` method, you can use IntelliJ’s code generation tool! Just
right-click within your class file and select
*Generate > equals and hashCode* and follow the prompts.

Let's use a ``Course`` class to demonstrate:

.. sourcecode:: java
   :linenos:

   public class Course {

      private String title;
      private int credits;
      private String instructor;

      public Course (String title, int credits, String instructor) {
         this.title = title;
         this.credits = credits;
         this.instructor = instructor;
      }
   }

#. In the IntelliJ editor, right-click in the editor (or on the ``Course``
   class name to be really deliberate), then select *Generate* from the menu.

   .. figure:: ./figures/IJgeneratemenu.png
      :scale: 80%
      :alt: Pop up menu for IntelliJ's generate option.

#. Select the *equals() and hashCode()* option:

   .. figure:: ./figures/selectEqualsOption.png
      :scale: 80%
      :alt: Select ``equals`` option.

#. Select the default options until you are asked to choose the fields you
   want ``equals`` to consider. Let's assume that two ``Course`` objects
   will be equal if they have the same ``title`` and ``instructor`` values.

   .. figure:: ./figures/chooseFields.png
      :alt: Select fields to compare.

#. Repeat the selections in the next two prompts for the ``hashCode`` and
   ``null`` fields.

#. Click *Finish*. IntelliJ generates the ``equals`` and ``hashCode`` methods:

   .. sourcecode:: java
      :linenos:

      import java.util.Objects;

      public class Course {

         private String title;
         private int credits;
         private String instructor;

         public Course (String title, int credits, String instructor) {
            this.title = title;
            this.credits = credits;
            this.instructor = instructor;
         }

         @Override
         public boolean equals(Object o) {
            if (this == o) return true;
            if (!(o instanceof Course)) return false;
            Course course = (Course) o;
            return title.equals(course.title) &&
                     instructor.equals(course.instructor);
         }

         @Override
         public int hashCode() {
            return Objects.hash(title, instructor);
         }
      }

Looking at the new ``equals`` method shows that it includes all of the
:ref:`best-practice components <components-of-equals>`:

#. Line 17 performs the reference check on the object ``o``.
#. Line 18 performs the ``null`` check and class check on ``o``.
#. Line 19 casts ``o`` as a ``Course`` object.
#. Line 20 compares the ``title`` and ``instructor`` fields of the two objects.

Try It!
--------

Use the *Generate* option to add getters, setters, and a ``toString`` method
to the ``Course`` class.

   COOL!!!!!
