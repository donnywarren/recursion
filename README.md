# Recursion

![](https://miro.medium.com/max/669/1*Hgviugi5d0AZcFgy1-xVqQ.jpeg)

### Objectives:

1. Define what recursion is and how it can be used
2. Call stack.
2. Understand the two essential components of a recursive function 
3. Visualize the call stack in order to understand recursive functions

### What is recursion? 

**Recursion is when a function calls itself.**

Recursion is used a lot in functional programming. 

JSON.parse and JSON.stringify are recursive functions. We will see that recursion is used a lot more with more complex data structures(graphs, binary trees). Ultimately, recursion is more elegant and cleaner way to perform iteration.

### The call stack. 

Before we dive deeper in the implementation of a recursive functions we want to understand what's happenning under the hood when functions are called in JS.
In almost all program languages there is a built-in data structure that manages the order in which functions are invoked. This data structure is called **call stack**. Anytime a function is invoked it is placed(pushed) on top of the call stack. When JS sees the `return` keyword, the function ends and it will be removed from the stack. 





### Summary

 A lot of the times, recursion make writing out code for our algorithm a bit easier and at times clearer. Any time you write a recursive function, though, keep in mind that it can be rewritten iteratively (or with a loop). In most cases, recursive functions are less efficient than iterative ones because we are adding a bunch of calls to the call stack. If we add too many function calls to the call stack we can have a stack overflow (this is usually around 20-40,000 calls)! Some languages do optimize tail recursion which essentially makes a recursive function into a while loop during interpreting or compiling.