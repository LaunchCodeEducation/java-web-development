.. _controllers-class-annotations:

Class Level Controller Annotations
==================================

Controller Classes - Video
--------------------------

.. youtube::
   :video_id: DvEvhB20e2s

.. admonition:: Note 

	The starter code for this video is found in the `forms branch <https://github.com/LaunchCodeEducation/hello-spring-demo/tree/forms>`__  
	of the ``hello-spring-demo`` repo. The final code presented in this video is found on the `class-annotations branch <https://github.com/LaunchCodeEducation/hello-spring-demo/tree/class-annotations>`__. 
	As always, code along to the videos on your own ``hello-spring`` project.

	Have you been tracking your app progress in your own 
	`git branches <https://education.launchcode.org/intro-to-professional-web-dev/chapters/git/branches.html?highlight=git%20checkout#creating-a-new-branch>`__? 
	Saving your progress in branches for each video tutorial 
	means you can always go back to a certain spot in the app development. 
	We will be returning to the ``forms`` branch in the next lesson so track your ``class-annotations`` in a new branch with 
	``git checkout -b <branch-name>``.
	


Controller Classes - Text
--------------------------

Once you have written several controller methods within a class, you may
notice some similar behavior across handlers. This is an opportunity to 
DRY your code. Some of the annotations we use at the method level can also 
be used on whole controller classes.

We mention this earlier. If all of the methods in a controller class begin 
with the same root path, ``@RequestMapping`` can be added above the class.

.. sourcecode:: java

   @Controller
   @RequestMapping(value="hello")
   public class HelloController {

      // responds to /hello
      @GetMapping("")
       @ResponseBody
       public String hello() {
        return "Hello";
       }

      // responds to /hello/goodbye
      @GetMapping("goodbye")
       @ResponseBody
       public String helloGoodbye() {
        return "Hello, Goodbye";
       }
   }

Note that we use ``@RequestMapping`` on the class. ``@GetMapping`` and ``@PostMapping``
cannot be applied at the class level.

In a related fashion, if you find that each of your methods in a controller class
use ``@ResponseBody`` to return plain text, this annotation may be added at the top 
of the class, rather than at each method declaration.

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: No one controller method can handle several request types.
 
   a. True
      
   b. False

.. ans: b, A controller method annotated with ``@RequestMapping`` can handle multiple request types.

.. admonition:: Question

   We want the method ``hello`` to take another parameter, ``@RequestParam String friend``, that will 
   add a friend's name to the returned greeting. The use should also be able to enter this name via 
   a text field. What needs to be added to the form?
 
   a. Another ``input`` tag with a ``friend`` attribute.

   b. Another ``input`` tag with a ``name`` attribute.

   c. Another ``form`` tag with a ``method`` attribute.

   d. Another ``submit`` tag with a ``friend`` value.

.. ans:  b, Another ``input`` tag with a ``name`` attribute.


