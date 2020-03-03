# Recursion

![](https://miro.medium.com/max/669/1*Hgviugi5d0AZcFgy1-xVqQ.jpeg)

## Objectives:

1. Define what recursion is and how it can be used.
2. Define the call stack.
2. Understand the two essential components of a recursive function.
3. Visualize the call stack in order to understand recursive functions.

## What is recursion? 

**Recursion is when a function calls itself.**

Recursion is used a lot in functional programming. 

JSON.parse and JSON.stringify are examples recursive functions. We will see that recursion is used a lot more with more complex data structures(graphs, binary trees). Ultimately, recursion is more elegant and cleaner way to perform iteration.

## What is the call stack?

Before we dive deeper in the implementation of a recursive functions we want to understand what's happening under the hood when functions are called in JS.

In almost all programming languages there is a built-in data structure that manages the order in which functions are invoked. This structure is called the **call stack**. Anytime a function is invoked, it is placed (pushed) to the top of the call stack. When JS sees the `return` keyword, the function ends, and it is removed from the stack. 

With recursion, we keep pushing the same function into to the call stack by instructing the function to invoke itself.

## Recursive Functions

Every recursive function has two parts:

 - **base case**
 - **recursive case**

A recursive function invokes itself with a different input (**recursive case**) until we reach our **base case** (exit condition). If we don't have a **base case** with a `return` keyword, the function will get stuck invoking itself in an infinite loop. 

If you happen to do this, the error you'd get would look something like that: 

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

This is also known as **stack overflow**. It's caused by excessively deep or infinite recursion– when a function calls itself so many times that the space needed to store the data (variables and information) associated with those calls are more than can actually fit on the stack.

[Stack Overflow Wikipedia](https://en.wikipedia.org/wiki/Stack_overflow)

### Let's see an example of a **pure** recursive function:

```
function sumRange(num) {
	if (num === 1) return 1;
	return num + sumRange(num-1);
}
```

* Find the base case 
* Finf the recursive case 

For comparison's sake, consider how the same function would be written with a more familiar loop :

```
function sumRange(num) {
   let count = 0;
   for(let i = 0; i <= num;i++) {
       count += i
   }
   return count;
}
```

What is actually happening when we call the recursive `sumRange` ? 

```
sumRange(3) 
    return 3 + sumRange(2) => 6 
        return 2 + sumRange(1) => 3
                		return 1 
```

### Now, how about examples of functions that implement helper methods recursion:

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
  
}

getTheOdds([143,457,675,899,324]) // ==> Your array of [143,457,675,899,324] containes 4 odd numbers - 143,457,675,899
getTheOdds([14,4,6,8,10]) // ==> You array doesn't have any odd numbers. Sorry!
```

## Summary

A lot of times, recursion can make programming algorithms a bit easier and clearer. Any time you write a recursive function, though, keep in mind that it can be rewritten iteratively (or with a loop).

In most cases, recursive functions are less efficient than iterative ones because we are adding exponentially more calls to the call stack. If we add too many function calls to the call stack, a stack overflow will break your program. (This is usually somewhere from 20,000 to 40,000 function invocations!)

Some languages do optimize **tail recursion** which essentially makes a recursive function into a while loop during interpreting or compiling.

## Exercises

```
function fizzBuzz(n, i=1) {

}

function reverseString() {
	// This function takes a string and reverses it recursively.
}

function findMax() {
	// This function returns the largest number in a given array.
}

function fibonacci() {
	// This function returns the Nth number in the fibonacci sequence.
	// https://en.wikipedia.org/wiki/Fibonacci_number
	// For this function, the first two fibonacci numbers are 1 and 1
}
```

