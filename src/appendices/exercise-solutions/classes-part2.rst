Exercise Solutions: Classes and Objects, Part 2
===============================================

The ``getGradeLevel`` Method
-----------------------------

This method returns the student's level based on the number of credits they
have earned: Freshman (0-29 credits), Sophomore (30-59 credits), Junior (60-89
credits), or Senior (90+ credits).

.. sourcecode:: java

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

``toString`` and ``equals``
---------------------------

#. Add custom ``equals()`` and ``toString()`` methods to the ``Student``
   class.

   .. sourcecode:: java

      public String toString(){
         String studentReport = String.format("%s is a %s with %d credits and a GPA of %.2f", this.name, this.getGradeLevel(this.numberOfCredits), this.getNumberOfCredits(), this.getGpa());
         return studentReport;
      }

      public boolean equals(Object toBeCompared){
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


