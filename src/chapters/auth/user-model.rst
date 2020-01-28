Creating a ``User`` Model
=========================

The next few sections walk through the steps necessary to enable simple authentication in the ``coding-events`` app. 

.. admonition:: Note

   While we'll use ``coding-events``, these steps would be the same for any other app. If you want to add simple authentication to a Spring Boot application in the future, reference this chapter.

Before we can authenticate users, we need users to authenticate! We'll start by adding a ``User`` model.

A ``User`` Model
----------------------

A model class representing users needs, at a minimum, fields representing username and password.

In the ``models`` package, create a ``User`` class with ``@Entity`` and extending ``AbstractEntity``. It should have two string fields, ``username`` and ``pwHash``. We only need a getter for ``username``.

.. sourcecode:: java
   :lineno-start: 13

   @Entity
   public class User extends AbstractEntity {

      @NotNull
      @NotBlank
      @Size(min = 0, max = 20, message = "Invalid username")
      private String username;

      @NotNull
      @NotBlank
      private String pwHash;

      public User() {}

      public User(String username, String password) {
         this.username = username;
         this.pwHash = password;
      }

      public String getUsername() {
         return username;
      }

   }

Notice that the constructor takes a parameter named ``password`` and uses it to set the value of ``pwHash``. We mentioned :ref:`previously <hashing-passwords>` that we should never store passwords, so in a moment we will create a hash from the given password to store.

Hashing Passwords
-----------------

.. index:: ! bcrypt

We'll use the bycrypt hash algorithm. One way to access this algorithm is via the following dependency:

:: 

   org.springframework.security:spring-security-crypto

Add this as an ``implementation`` dependency in your ``build.gradle`` file. 

This dependency provides the ``BCryptPasswordEncoder`` class, which we will use to create and verify hashes. While our class needs one of these encoder objects, it does not need to be an instance variable. We'll make it static so it can be shared by all ``User`` objects.

.. sourcecode:: java
   :lineno-start: 25

   private static final BCryptPasswordEncoder encoder = new BCryptPasswordEncoder();

In the constructor, we can use ``encoder`` to create a hash from the given password:

.. sourcecode:: java
   :lineno-start: 29

   public User(String username, String password) {
      this.username = username;
      this.pwHash = encoder.encode(password);
   }

Our ``User`` objects should also be responsible for determining if a given password is a match for the hash stored by the object. We can do this using the ``encoder.matches()`` method. Let's put this behavior in a method at the bottom of our ``User`` class:

.. sourcecode:: java
   :lineno-start: 38

   public boolean isMatchingPassword(String password) {
      return encoder.matches(password, pwHash);
   }

Creating the ``UserRepository``
-------------------------------

As usual, we need a repository in order to access ``User`` objects stored in the database. This time, however, we add a twist. Create ``UserRepository`` in the ``data`` package, with the following contents:

.. sourcecode:: java
   :lineno-start: 9

   public interface UserRepository extends CrudRepository<User, Integer> {

      User findByUsername(String username);

   }

.. index:: ! query methods

While our repository extends ``CrudRepository``, it also contains a new method, ``findByUsername``. Based on the method signature, it appears that this method is intended to take a username, and return the given user with that username. Indeed, when our application runs, the ``UserRepository`` will have such a method.

Spring allows for additional, custom methods to be added to repository interfaces, as long as they follow some basic naming conventions. These conventions are straightforward to use, and allow you to create additional, more sophisticated query methods. Methods created in this way are called **query methods**, and their rules are defined in `Spring's documentation <https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation>`_.


