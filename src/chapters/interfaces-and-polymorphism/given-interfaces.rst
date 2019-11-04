Interfaces In The Wild
----------------------

The most immediate situations that you’ll encounter in which you’ll want
to use interfaces are when working with interfaces and classes that are
part of Java. Here are just a few.

Comparable<T>
~~~~~~~~~~~~~

**Purpose**: A class implements ``Comparable<T>`` in order to allow
comparison - in a “greater than” and “less than” sense - to another
instance of the class. This is a “parameterized” interface, which means
that when using it you need to specify the class that it will be
comparing. For example, ``Comparable<Job>`` would compare ``Job``
objects.

**Important Methods**: ``compareTo(T)``

`Comparable<T>
Documentation <http://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html>`__

Comparator<T>
~~~~~~~~~~~~~

**Purpose**: Compare two objects of a given class. When wanting to
compare objects from a given class, you can create several different
``Comparator`` classes to allow different types of comparison and
ordering. The class that you want to compare objects of *does not*
implement the interface itself.

**Important Methods**: ``compare(T, T)``

`Comparator<T>
Documentation <http://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html>`__

This interface can be used to determine, given two objects of the given
type, which one is “greater” than the other. It is also used by
collections such as
`ArrayList <http://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html>`__
to sort its contents with the
`sort <http://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html#sort-java.util.Comparator->`__
method.

.. raw:: html

   <aside class="aside-note">

For more on the differences between ``Comparator`` and ``Comparable``,
see `this
article <https://www.javatpoint.com/difference-between-comparable-and-comparator>`__.

.. raw:: html

   </aside>

Iterable<T>
~~~~~~~~~~~

**Purpose**: Enable iteration over a collection of objects using a
for-each loop

**Important Methods**: ``iterator()``

`Iterable<T>
Documentation <http://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html>`__

This interface is implemented by the ``ArrayList<T>`` class, which we’ve
been using throughout this course.

**Example**

.. code:: java

   Iterable<String> collection = new ArrayList<>();

   // Add items to the collection

   for (String item : collection) {
       // do something with each item
   }

List<T>
~~~~~~~

**Purpose**: Enable access to objects in a collection by index. In other
words, enable ordered collections.

**Important Methods**: ``add(int, T)``, ``get(int)``, ``indexOf(T)``

`List<T>
Documentation <http://docs.oracle.com/javase/8/docs/api/java/util/List.html>`__

This interface is also implemented by the ``ArrayList<T>`` class, which
we’ve been using throughout this course. In fact, ``List<T>`` extends
``Iterable<T>``. *An interface may extend another interface*, in the
same way that classes may extend each other.

**Example**

.. code:: java

   List<String> collection = new ArrayList<>();

   // Add items to the collection

   // Get the first item
   String firstItem = collection.get(0);

Map<K, V>
~~~~~~~~~

**Purpose**: Represent a collection of key/value pairs.

**Important Methods**: ``get(K)``, ``containsKey(K)``, ``put(K, V)``

`Map<K, V>
Documentation <http://docs.oracle.com/javase/8/docs/api/java/util/Map.html>`__

This interface is implemented by the ``HashMap<K, V>`` class, which
we’ve been using throughout this course.

**Example**

.. code:: java

   Map<String, String> collection = new HashMap<>();

   // Add items to the collection

   // Get item with key "hello"
   String hello = collection.get("hello");

Default Methods
~~~~~~~~~~~~~~~

We mentioned above that we would introduce **default methods**, so let’s
do that now. A default method has a body. In other words, it is a
fully-formed method. It is preceded with the ``default`` keyword, and it
may be overridden by classes implementing the interface.

.. code:: java

   public interface MyInterface {

       void someMethod();

       default void someOtherMethod() {
           // ...code goes here...
       }

   }

Default methods were added to Java 8 (the most recent version of Java),
and thus are relatively new. Their intended purpose is to allow
programmers to add a method to an interface that has already been
released, while not forcing those already using the interface to add new
code to their classes. You should avoid using default methods in all
other situations other than the one described here. *Do not use default
methods when writing a new interface.*