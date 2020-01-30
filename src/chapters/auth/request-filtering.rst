Filtering Requests
==================

Our application now allows users to register and log in. However, access to pages on the site is NOT yet restricted in any way. Even if a user isn't logged in, they may view any page on the site. To fully implement authentication, we need to be able to check a user's login status on each request, *before* any controller methods are called.

.. index:: ! request filtering

We can do this by filtering requests. **Request filtering** is a mechanism available in many web frameworks. It allows a programmer to carry out certain actions before any controllers are called.

Request Filters in Spring
-------------------------

A request filter in Spring can be built by extending the built-in class ``HandlerInterceptorAdapter`` and overriding one of its various methods. This class implements an interface called ``HandlerInterceptor``, which `specifies a few methods <https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/servlet/HandlerInterceptor.html>`_ that are called during the request-handling process:

- ``preHandle`` - called *before* a request is handled by a controller
- ``postHandle`` - called *after* a request is handled by a controller, but *before* the view is rendered
- ``afterCompletion`` - called *after* the view is rendered

By extending ``HandlerInterceptorAdapter`` and overriding one or more of these methods, we can write code that is executed at a specific point of *every* request to our application. This is exactly what we need to implement authentication. More specifically, we will override ``preHandle`` and check for a user's login status.

Creating ``AuthenticationFilter``
---------------------------------

In the top-level package of the app, ``org.launchcode.codingevents``, create a class named ``AuthenticationFilter`` that extends ``HandlerInterceptorAdapter``. 

This class will need to access user data, so autowire a ``UserRepository`` field. We will also need to use the ``AuthenticationController.getUserFromSession`` method, so autowire an ``AuthenticationConroller`` field as well.

.. sourcecode:: java
   :lineno-start: 19

   public class AuthenticationFilter extends HandlerInterceptorAdapter {

      @Autowired
      UserRepository userRepository;

      @Autowired
      AuthenticationController authenticationController;

   }

.. admonition:: Note

   For autowiring to work, a class must be Spring-managed. There are many ways a given class may registered as a Spring-managed class, but any class with ``@Controller`` will be automatically registered. Thus, any controller class may be autowired.

Overriding ``preHandle``
^^^^^^^^^^^^^^^^^^^^^^^^

Here is our initial ``preHandle`` method, with a detailed breakdown below.

.. sourcecode:: java
   :lineno-start: 27

   @Override
   public boolean preHandle(HttpServletRequest request,
                           HttpServletResponse response,
                           Object handler) throws IOException {

      HttpSession session = request.getSession();
      User user = authenticationController.getUserFromSession(session);

      // The user is logged in
      if (user != null) {
         return true;
      }

      // The user is NOT logged in
      response.sendRedirect("/login");
      return false;
   }

The signature of our method must match the `definition of preHandle <https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/servlet/HandlerInterceptor.html#preHandle-javax.servlet.http.HttpServletRequest-javax.servlet.http.HttpServletResponse-java.lang.Object->`_ and ``HandlerInterceptor`` *exactly*, even if we don't need all of the parameters. We will only use the ``request`` argument, but we still need to include the ``response`` and ``handler`` arguments.

.. admonition:: Note

   The sharp-eyed reader will notice that our ``preHandle`` and the overridden method in ``HandlerInterceptor`` throw different exception types. This is the one way in which the method signatures are allowed to differ, so long as the exception type of our method is a subclass of the overridden method. Since ``IOException`` extends ``Exception``, this is allowed. 

Notice that ``preHandle`` returns a boolean. The return value will dictate what happens after the handler finishes running. If we return ``true``, then request processing will continue as normal, with the appropriate controller method being called. If we return ``false``, then processing will halt, and no controllers will be called.

Let's break down this method.

- **Line 32**: Retrieves the user's ``session`` object, which is contained in the ``request``.
- **Line 33**: Retrieves the ``User`` object corresponding to the given user. Recall that this will be ``null`` if the user is not logged in.
- **Lines 36-38**: The ``user`` object is non-null, so the user is logged in. Allow the request to be handled as normal.
- **Lines 41-42**: The ``user`` object is ``null``, so we redirect the user to the login page.

This method has the effect of preventing access to *every* page on the app if a user is not logged in. This creates one not-so-minor problem: How will a user access the login page if they are not logged in?

Creating a Whitelist
^^^^^^^^^^^^^^^^^^^^

.. index:: ! whitelist

The term **whitelist** often refers to a list of items that are NOT subject to a given restriction. For our filter to fully work, we need a whitelist of pages that may be accessed by *any* user, regardless of whether or not they are logged in.

Let's define our whitelist above ``preHandle``:

.. sourcecode:: java
   :lineno-start: 27

   private static final List<String> whitelist = Arrays.asList("/login", "/register", "/logout");

At minimum, users should be able to access the routes associated with logging in and out. Depending on the desired use-cases for your application, you may want to add additional pages to the whitelist. For example, many web apps have a home page that does not require being logged in to view. 

We now need a way to check whether or not a given request is whitelisted. The following utility method does the trick:

.. sourcecode:: java
   :lineno-start: 29

   private static boolean isWhitelisted(String path) {
      for (String pathRoot : whitelist) {
         if (path.startsWith(pathRoot)) {
               return true;
         }
      }
      return false;
   }

This method takes a string representing a URL path and checks to see if it *starts with* any of the entries in ``whitelist``. If you wanted to be more restrictive, you could use ``.equals()`` instead of ``.startsWith()``. If the path is whitelisted, we return true. Otherwise, we return false.

We can now check all requests against the whitelist within ``preHandle``:

.. sourcecode:: java
   :lineno-start: 38

   @Override
   public boolean preHandle(HttpServletRequest request,
                           HttpServletResponse response,
                           Object handler) throws IOException {

      // Don't require sign-in for whitelisted pages
      if (isWhitelisted(request.getRequestURI())) {
         // returning true indicates that the request may proceed
         return true;
      }

      HttpSession session = request.getSession();
      User user = authenticationController.getUserFromSession(session);

      // The user is logged in
      if (user != null) {
         return true;
      }

      // The user is NOT logged in
      response.sendRedirect("/login");
      return false;
   }

``request.getRequestURI()`` returns the request path (see `the docs <https://javaee.github.io/javaee-spec/javadocs/javax/servlet/http/HttpServletRequest.html>`_ for more details). Lines 43-47 check the path against the whitelist, returning true (that is, allowing the request to proceed) if the path is whitelisted. 

With our filter complete, we simply need to let Spring know about it to complete our authentication code.

Registering the Filter With Spring
----------------------------------

.. index:: ! code-based configuration

Spring Boot uses **code-based configuration**, which means that many application configurations can be done using Java classes. We'll use code-based configuration to register our filter.

At the top-level package of the app, ``org.launchcode.codingevents``, create a class named ``WebApplicationConfig`` with the code below:

.. sourcecode:: java
   :lineno-start: 11

   @Configuration
   public class WebApplicationConfig implements WebMvcConfigurer {

      // Create spring-managed object to allow the app to access our filter
      @Bean
      public AuthenticationFilter authenticationFilter() {
         return new AuthenticationFilter();
      }

      // Register the filter with the Spring container
      @Override
      public void addInterceptors(InterceptorRegistry registry) {
         registry.addInterceptor( authenticationFilter() );
      }

   }

The ``@Configuration`` annotation flags this class to Spring as one that contains configuration code. By implementing ``WebMvcConfigurer``, we ensure that Spring will call our ``addInterceptors`` method during startup, giving us the chance to register our filter. 

The first method---``authenticationFilter``, which is annotated with ``@Bean``---makes our filter available as a Spring-managed class. 

Now you can start your application and test. You should be required to log in to view anything other than login and registration pages. 

The code for this section is available in the `auth-filter branch <https://github.com/LaunchCodeEducation/coding-events/tree/auth-filter>`_ of the ``coding-events`` repository.

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: Request filtering takes place before any controller is called.

   #. True
   #. False

.. ans: True

.. admonition:: Question

   True/False: When our code checks a path against entries in the whitelist, 
   it must match exactly in order for the path to be accessed without logging in.

   #. True
   #. False

.. ans: False, Whitelisted paths as listed in this application can be just a root address.

