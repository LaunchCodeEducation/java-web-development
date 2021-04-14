.. _classes-exercise-solutions:

Exercise Solutions: Classes and Objects
=======================================

#. Open up the file, ``Student.java``, and add all of the necessary getters and
   setters. Think about the access level each field and method should have, and
   try reducing the access level of at least one setter to less than public.

   .. sourcecode:: java

      public Student (String name, int studentId, int numberOfCredits, double gpa) {
      this.name = name;
      this.studentId = studentId;
      this.numberOfCredits = numberOfCredits;
      this.gpa = gpa;
      }

      public void setName(String name) {
      this.name = name;
      }

      public void setStudentId(int studentId) {
      this.studentId = studentId;
      }

      public void setGpa(double gpa) {
      this.gpa = gpa;
      }

      private void setNumberOfCredits(int numberOfCredits) {
      this.numberOfCredits = numberOfCredits;
      }

      public String getName() {
      return name;
      }

      public int getStudentId() {
      return studentId;
      }

      public int getNumberOfCredits() {
      return numberOfCredits;
      }

      public double getGpa() {
      return gpa;
      }

      public static void main(String[] args) {
      Student sally = new Student("Sally",1,1,4.0);
      System.out.println("The Student class works! " + sally.getName() + " is a student!");
      }

3. In the ``school`` package, create a class ``Course`` with at least three fields. Before diving into IntelliJ, try using pen and paper to work through what these might be. At least one of your fields should be an ``ArrayList`` or ``HashMap``, and you should use your ``Student`` class.

   .. sourcecode:: java

      public class Course {
      private String topic;
      private Teacher instructor;
      private ArrayList<Student> enrolledStudents;
      }

