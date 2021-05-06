.. _classes2-exercise-solutions:

Exercise Solutions: Classes and Objects, Part 2
===============================================

.. _classes2-exercise-solutions1:

The ``getGradeLevel`` Method
-----------------------------

This method returns the student's level based on the number of credits they
have earned: Freshman (0-29 credits), Sophomore (30-59 credits), Junior (60-89
credits), or Senior (90+ credits).

.. sourcecode:: java
   :linenos:

   public static String getGradeLevel(int credits) {
      if (credits <= 29){
         return "freshman";
      } else if (credits <= 59){
         return "sophomore";
      } else if (credits <= 89) {
         return "junior";
      } else {
         return "senior";
      }
   }

:ref:`Back to the exercises <classes-exercises-part2>`

.. _classes2-exercise-solutions2:
   
The ``addGrade`` Method
------------------------

This method accepts two parameters---a number of course credits and a
numerical grade (0.0-4.0). With this data, you need to update the student’s
GPA.

GPA Information
^^^^^^^^^^^^^^^^

GPA is computed via the formula:

   gpa = (total quality score) / (total number of credits)

#. The *quality score* for a class is found by multiplying the letter grade
   score (0.0-4.0) by the number of credits.
#. The *total quality score* is the sum of the quality scores for all classes.

For example, if a student received an "A" (worth 4 points) in a 3-credit course
and a "B" (worth 3 points) in a 4-credit course, their total quality score
would be: 4.0 * 3 + 3.0 * 4 = 24. Their GPA would then be 24 / 7 = 3.43.

Determine the New GPA
^^^^^^^^^^^^^^^^^^^^^^

To update the student's GPA:

#. Calculate their *current* total quality score by using the formula
   ``gpa * numberOfCredits``.
#. Use the new course grade and course credits to update their total quality
   score.
#. Update the student's total ``numberOfCredits``.
#. Compute their new GPA.

.. sourcecode:: java
   :linenos:

   public void addGrade(int courseCredits, double grade) {
      double totalQualityScore = this.gpa * this.numberOfCredits;
      totalQualityScore += courseCredits * grade;
      this.numberOfCredits += courseCredits;
      this.gpa = totalQualityScore/this.numberOfCredits;
   }

:ref:`Back to the exercises <classes-exercises-part2>`

.. _classes2-exercise-solutions3a:

``toString`` and ``equals``
---------------------------

#. Add custom ``equals()`` and ``toString()`` methods to the ``Student``
   class.

   .. sourcecode:: java
      :linenos:

      public String toString() {
         String studentReport = String.format("%s is a %s with %d credits and a GPA of %.2f", this.name, this.getGradeLevel(this.numberOfCredits), this.getNumberOfCredits(), this.getGpa());
         return studentReport;
      }

      public boolean equals(Object toBeCompared) {
         if (toBeCompared == this) {
            return true;
         }

         if (toBeCompared == null) {
            return false;
         }

         if (toBeCompared.getClass() != getClass()) {
            return false;
         }

         Student theStudent = (Student) toBeCompared;
         return theStudent.getStudentId() == getStudentId();
      }

:ref:`Back to the exercises <classes-exercises-part2>`

