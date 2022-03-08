Studio: If It Ain't Broke, Add a Breakpoint!
============================================

On your machine, open up your copy of ``lsn7interfaces`` in IntelliJ. 
The purpose of this studio is to talk about your current debugging strategies 
and how to make the most of the debugger tools discussed in this chapter.

Before we start practicing with debugging tools, 
review with the group one error you encountered when working on your version of lesson 7’s studio. 
This could be the result of a typo or a logical error.

#. What was the error?
#. How did you solve this error? What strategies and tools have you been using so far to debug your code?
#. Could one of the debugging tools help you when addressing this error?

Now, check out the debugging branch of the studio repo. 
Review the code and then practice using IntelliJ's debugging tools.
To get started, try the following:

#. Add a few breakpoints inside ``Main.java`` and then make a note of where you expect the program to break in its execution.
#. Add ``cd.name`` as a *Watch expression* in the *Variables Pane* of the Debugger.
#. Add a breakpoint inside some of the methods in ``BaseDisc.java``.  Anticipate what you expect to see as the last line in the *Variables Pane*  when the debugger stops.

After you look through the code and try out these tasks above, take it one step further by answering these questions.

#. When would use a *Watch expression*?  If you run the app and it's already functioning, what shows up there?
#. Would a conditional breakpoint make sense to use in the context of this app? Try adding a conditional breakpoint and then run your app.
#. What does the *Frames Pane* tell you as you step through your code?
#. Add ``dvd.aName`` as a *Watch expression* and add a breakpoint.  Can you explain the output in the *Variables Pane*?

Once you have gone through the code, open up a piece of code you have been struggling with.
In what ways could you make use of the debugging tools to help you figure out what is going on with the code?
 
**Additional Resources for IntelliJ's Debugger**

- `Debug code <https://www.jetbrains.com/help/idea/debugging-code.html#df9fd13c>`_
- `Tutorial: Debug your first Java application <https://www.jetbrains.com/help/idea/debugging-your-first-java-application.html>`_