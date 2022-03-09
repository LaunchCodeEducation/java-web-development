Debugging in IntelliJ
=====================

.. youtube::
   :video_id: 1bCgzjatcr4

Watch this video to learn the basics of the debugging tools available in IntelliJ.
If you want to follow along, Chris is working with ``ArrayListGradebook`` 
from the :ref:`Control Flow and Collections <array-list>` chapter 
and the ``HelloMethods`` and ``Message`` from  :ref:`Classes and Objects, Part 2 <static-methods-demo>` chapter.
You should have already downloaded this code from the ``java-web-dev-exercises``.  

.. admonition:: Note

   The video is using an older version of IntelliJ.  

   The overall functionality of the debugging pane is still there, however, 
   you may have to explore the location of buttons.  
   We recommend hovering over each icon and looking at the names of each.

   IntelliJ has `documentation and videos <https://www.jetbrains.com/help/idea/debugging-code.html#df9fd13c>`_ exploring their debugger if you are curious.

Steps to Find and Diagnose Logical Bugs
--------------------------------------- 

- Set a **breakpoint** where you want to pause the execution of the code. This will provide a more detailed look at what the program is doing at this point.  Right-click in the text editing window to add a breakpoint to your code.
- Run your program in **Debug** mode
- Inspect the values of your variables in the **Debugger Pane**.
- If needed, use the **Add/Watch** button to watch a specific expression as your program executes.
- You can also set a **conditional breakpoint** to pause the execution of the code when a certain condition is a method.

Control the Flow of Execution
-----------------------------

- **Step-over** button executes a given line then steps to the next executable line
- **Step-into** button allows you to review a called method and see what is going to line within the method
- **Step-out-of** button allows you to move out of the method you stepped into and resume stepping through the main code
- **Variables Pane** allows you to examine how variables are manipulated within your code.  Also allows you to identify specific *Watch expressions*
- **Frames Pane** tracks any method calls and threads in your code line by line.  Best used with breakpoints.


Advantage of Debugger Over Printing to the Console
--------------------------------------------------

- The debugger lets you look at **all** the values in your program instead of just guessing which values you want to track via logging to the console.


Check Your Understanding
------------------------

.. admonition:: Question

   What is a breakpoint?

   a.   A point in our code where the debugger will stop running and provide information about the current state.
   b.   A point in our code that we anticipate will result in an exception or error.
   c.   A point in our code where we include a print statement to see what’s going on.
   d.   A point in our code where we want to throw the computer out of a window because nothing works.