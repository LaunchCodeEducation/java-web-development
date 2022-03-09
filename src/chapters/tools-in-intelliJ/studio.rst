Studio: If It Ain't Broke, Add a Breakpoint!
============================================

The purpose of this studio is to expand your current debugging strategies.
First, as a group, you will discuss your current debugging strategies.
Next, you will explore the debugger tools addressed in this chapter.

This studio will use a previous studio assignment to explore IntelliJ's Debugger.
On your machine, open up your copy of `java-web-dev-studio7 <https://github.com/LaunchCodeEducation/java-web-dev-studio7>`_ in IntelliJ.



Part One: Pre-Debugger Debugging
--------------------------------

Review with the group one error you encountered when working on your version of lesson 7’s studio.
This could be the result of a typo or a logical error.

#. What was the error?
#. How did you solve this error?
#. What strategies and tools have you been using so far to debug your code?
#. Could one of the debugging tools help you when addressing this error?


Part Two: Debugger Debugging
----------------------------

Now, check out the ``debugging`` branch of the studio repo.
Review the code and then practice using IntelliJ's debugging tools.
To get started, try the following:

#. Add a few breakpoints inside ``Main.java``.  Make a note of where you expect the program to break in its execution.
#. Add ``cd.name`` as a *Watch expression* in the *Variables Pane* of the Debugger.
#. Add a breakpoint inside some of the methods in ``BaseDisc.java``.  Anticipate what you expect to see as the last line in the *Variables Pane*  when the debugger stops.


Part Three: More Debugger Debugging
-----------------------------------

Take your debugging skills one step further by answering these questions.

#. When would use a *Watch expression*?  If you run the app and it's already functioning, what shows up there?
#. Would a conditional breakpoint make sense to use in the context of this app? Try adding a conditional breakpoint and then run your app.
#. What does the *Frames Pane* tell you as you step through your code?
#. Add ``dvd.aName`` as a *Watch expression* and add a breakpoint.  Can you explain the output in the *Variables Pane*?


Part Four: Debugging Beyond This Studio
---------------------------------------

Once you have worked through the studio’s codebase, open up a piece of code you have been struggling with.
In what ways, could the debugging tools help you figure out what is going on with the code?


**Additional Resources for IntelliJ's Debugger**

- `Debug code <https://www.jetbrains.com/help/idea/debugging-code.html#df9fd13c>`_
- `Tutorial: Debug your first Java application <https://www.jetbrains.com/help/idea/debugging-your-first-java-application.html>`_
