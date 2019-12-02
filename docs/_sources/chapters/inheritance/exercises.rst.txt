Exercises: Inheritance
======================

Work on these exercises in the IntelliJ ``java-web-dev-exercises`` project. Add a new package called ``technology`` to your ``exercises`` directory.

1. **Class design:** Create a new class called ``Computer``. Before you add any more code, know that you will need to add two additional classes: ``Laptop`` and ``SmartPhone``.
   Before you start coding anything inside these classes, diagram how the three classes are going to be related to each other. 
   Remember to add properties and methods to your diagram!

   1. For a parent class add 3 properties, 2 methods, and a constructor.
   2. For a child class add *at least* 1 additional property and 1 additional method.

2. **Class implementation:** Implement your design and test it in a ``Program.java`` class.
   
   1. Try to add three JUnit tests per class!

3. **Abstract class design:** Consider the group of classes that you designed. Suppose you had a web program that used these classes, and you needed to assign a unique ID to every object created from one of these classes within the application. Therefore, each such class should have an ``Id`` property, and no two objects created from any of the classes may have the same value for ``Id``. Create an abstract class, ``AbstractEntity``, that contains the behavior for assigning and accessing such a unique ID for each class that extends it. Add this class to your program above, and add ``AbstractEntity`` to the class hierarchy in the correct place.

