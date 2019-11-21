Class Level Controller Annotations
==================================

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

