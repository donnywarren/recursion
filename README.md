# Recursion

![](https://miro.medium.com/max/669/1*Hgviugi5d0AZcFgy1-xVqQ.jpeg)

### Objectives:

1. Define what recursion is and how it can be used.
2. The call stack.
2. Understand the two essential components of a recursive function.
3. Visualize the call stack in order to understand recursive functions.

### What is recursion? 

**Recursion is when a function calls itself.**

Recursion is used a lot in functional programming. 

JSON.parse and JSON.stringify are recursive functions. We will see that recursion is used a lot more with more complex data structures(graphs, binary trees). Ultimately, recursion is more elegant and cleaner way to perform iteration.

### The call stack. 

Before we dive deeper in the implementation of a recursive functions we want to understand what's happenning under the hood when functions are called in JS.
In almost all program languages there is a built-in data structure that manages the order in which functions are invoked. This data structure is called **call stack**. Anytime a function is invoked it is placed(pushed) on top of the call stack. When JS sees the `return` keyword, the function ends and it will be removed from the stack. 

With recursion we keep pushing the same function over and over again to the call stack.

## Recursive function 
Every recirsive function has two parts: 
 - **base case**
 - **recursive case**

A recursive function invokes itsefl with a different input(**recursive case**) until we reach our **base case**(exit condition). If we don't have a **base case** with a `return` keyword, we will be stuck in an infinite loop. The error you will get would look something like that: 

```
VM2036 sumRange:1 Uncaught RangeError: Maximum call stack size exceeded
    at sumRange (VM2036 sumRange:1)
    at sumRange (VM2036 sumRange:3)
    at sumRange (VM2036 sumRange:3)
    at sumRange (VM2036 sumRange:3)
    at sumRange (VM2036 sumRange:3)
    at sumRange (VM2036 sumRange:3)
    at sumRange (VM2036 sumRange:3)
    at sumRange (VM2036 sumRange:3)
    at sumRange (VM2036 sumRange:3)
    at sumRange (VM2036 sumRange:3)
```

This is also known as **stack overflow** and it is caused by excessively deep or infinite recursion, in which a function calls itself so many times that the space needed to store the variables and information associated with each call is more than can fit on the stack.

[Stack Overflow Wikipedia](https://en.wikipedia.org/wiki/Stack_overflow)

#### Example of **pure** recursive function:

```
function sumRange(num) {
	if (num === 1) return 1;
	return num + sumRange(num-1);
}
```
* Find the base case 
* Finf the recursive case 

> The same function written with regular `for` loop: 

```
function sumRange(num) {
   let count = 0;
   for(let i = 0; i <= num;i++) {
       count += i
   }
   return count;
}
```
What is happening under the hood when we call the recursive sumRange ? 

```
sumRange(3) 
    return 3 + sumRange(2) => 6 
        return 2 + sumRange(1) => 3
                		return 1 
```

#### Example of functions that implement helper methods recursion.

```
function outer(input) {
  let array = [];
	  
  function helper(helperInput) {
	  if (helperInput.length === 0) {
	      return;
	  } else {
	    array.push(helperInput.substr(0))
	  }
	  helper(helperInput.slice(1))
  }
	  
  helper(input)
  
  return array;
}

outer("Svetla") ==> // [ 'Svetla', 'vetla', 'etla', 'tla', 'la', 'a' ]

```

```
function getTheOdds(input) {
  let array = [];
  let count = 0;
  function helper(helperInput) {
	  if (helperInput.length === 0) {
	      return;
	  } else {
	    if (helperInput[0] % 2 !== 0) {
	    	array.push(helperInput[0])
        count++
	    }
	  }
	  helper(helperInput.slice(1))
  }
	  
  helper(input)
  if (array.length > 0) {
    return `Your array of [${input}] containes ${count} odd numbers - ${array}`
  } else {
    return `You array doesn't have any odd numbers, ${count} of them.Sorry`
  }
  return array;
}

getTheOdds([143,457,675,899,324]) // ==> Your array of [143,457,675,899,324] containes 4 odd numbers - 143,457,675,899
getTheOdds([14,4,6,8,10]) // ==> You array doesn't have any odd numbers, 0 of them.Sorry
```

### Summary

 A lot of the times, recursion make writing out code for our algorithm a bit easier and at times clearer. Any time you write a recursive function, though, keep in mind that it can be rewritten iteratively (or with a loop). In most cases, recursive functions are less efficient than iterative ones because we are adding a bunch of calls to the call stack. If we add too many function calls to the call stack we can have a stack overflow (this is usually around 20-40,000 calls)! Some languages do optimize **tail recursion** which essentially makes a recursive function into a while loop during interpreting or compiling.