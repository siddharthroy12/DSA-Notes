# My notes on DSA and leetcode questions

I'm making my detailed notes here as I'm re-learning DSA. This can be useful to you even if you don't have any knowledge of DSA.

Contributions are welcomed.

## Table of Contents
1. [Big O](#big-o)
    1. [How to calculate Big O](#how-to-calculate-big-o)
    2. [Space Complexity](#space-complexity)
    3. [Big O Cheat Sheet](#cheat-sheet)
2. [Data Structures](#data-structures)
    1. [Arrays](#array)
    2. [Hash Tables](#hash-tables)
    3. [Linked List](#linked-list)
    4. [Stacks and Queues](#queues)
    5. [Trees](#trees)
    6. [Graphs](#graphs)
3. [Algorithms](#algorithms)
    1. [Sorting](#sorting)
    2. [BFS and DFS](#bfs-and-dfs)
    3. [Dynamic Programming](#dynamic-programming)
4. [Coding Problems](#coding-problems)

## Big O

The Big O notation is used to show how well an algorithm scales in terms of speed and space as the input grows.

It indicates how much time and memory an algorithm will take to solve an problem for a given input.

Because a code can run faster or slower on different processors it's not a good way to calculate the efficency of a program. 

That's why we use Big O notation to show how well a code performs when the input grows.

Big O can also be plotted to a graph:

![Big O Graph](./Big-O-Graph.png)

### How to caculate Big O

To calculate Big O we need to calculate how many operations the code/function/program will take for the given input.

For example this code:

```js
function getFirstElement(array) {
    return array[0];    // -- O(1)
}
```

This code returns the first element of an array so it has only one operation so the Big O of this function is O(1).

Let's look at another example:

```js
function sumOfFirstTheeElements(array) {
    let res = 0;    //  -- O(1)

    for (let i = 0; i < 3; i++) {   // -- O(3)
        res += array[i];
    }

    return res;   // -- O(1)
}
```

You might think the Big O of this function is O(5) because there are five operations in this code.

Which is correct but as the input grows the number of operations stays the same, it does not grow.

So it's a linear time which when denote as O(1).


Let's look at a code where numeber of operation grows as the input:

```js
function getIndexOf(array, element) {
    for (let i = 0; i < array.length; i++) { // -- O(n)
        if (array[i] === element) {
            return i;
        }
    }
}
```

This code will find the index of an element in a array by looping over each element.

So in the best case if the element is at the first index it will only do one operation O(1) but in the worst case the number of operations will be equal to the number of inputs which it denoted by O(n).

When we calculate the Big O we are always take the worst case so the Big O of this code is O(n).

Let's look at a another similar example:

```js
function getIndexOfArrayAndSumOfFirstThree(array, element) {
    let index = 0;
    let sum = 0;

    for (let i = 0; i < array.length; i++) { // -- O(n)
        if (array[i] === element) {
            index = i;
            break;
        }
    }
    
    for (let i = 0; i < 3; i++) {   // -- O(3)
        sum += array[i];
    }

    return { index, sum };
}
```

Here we have a function that does two things:
    - Get the index of an element
    - Get the sum of first three element

You might think that the Big O of this function is O(n) + O(3) = O(n+3). But we don't count the constant numbers like 3 because if the number of elements is 1000 then having extra 3 operation doesn't matter to us, so we remove the constant and this becomes O(n).

> In big tech we often work with big amount of data


But what if we have two for loops?

```js
function getSumAndMultipleOfElements(array) {
    let sum = 0;
    let multiple = 0;
    
    for (let i = 0; i < array.length; i++) {   // -- O(N)
        sum += array[i];
    }

    for (let i = 0; i < array.length; i++) {   // -- O(N)
        multiple *= array[i];
    }

    return { sum, multiple };
}
```

We have to O(n) here so it should become O(2n) right?

Even though the graph of this is steeper than O(n) it's still a straight line (a linear graph), so once again we remove the constant and it becomes O(n).

For two separate collection:

```js
function getSumOfTwoArray(array1, array2) {
    let sum1 = 0;
    let sum2 = 0;

    for (let i = 0; i < array.length; i++) {   // -- O(N)
        sum1 += array1[i];
    }

    for (let i = 0; i < array.length; i++) {   // -- O(N)
        sum2 += array2[i];
    }

    return { sum1, sum 2};
}
```

People often confuse this as O(n) but this is incorrect. Because we have two inputs we need show two variables in the notation. So this is O(a+b).


For nested loops:
```js
function getPairsOfElements(array) {
    let res = [];

    for (let i = 0; i < array.length; i++) {   // -- O(N)
        for (let j = 0; j < array.length; j++) {   // -- O(N)
            res.push([i,j]);
        }
    }

    return res;
}
```

For nested loops like this we just multiply the operations, so this becomes O(n*n) = O(n^2).

And the last rule:
Drop Non-dominant terms

```js
function getSumAndPairs(array) {
    let pairs = [];
    let sum = 0;

    for (let i = 0; i < array.length; i++) {   // -- O(N)
        for (let j = 0; j < array.length; j++) {   // -- O(N)
            pairs.push([i,j]);
        }
    }

    for (let i = 0; i < array.length; i++) {   // -- O(N)
        sum += array1[i];
    }
}
```

This looks like it has complexity of O(n + n^2) but because n^2 is way more important than n because it grows much faster than n.

When calculate Big O we are concerned about the scalibility of the function and not the accurate speed of the function.

### Space complexity

Big O is not only used to calculate time compexity it also used to calculate memory usage.

And there is relation between time and memory usage in computers.

If an algorithm uses less time then It will have to use more memory, If an algorithm uses less memory then it will take more time to perform.

You cannot have the best of both worlds.

If you are writing a software that runs on low-end systems (like mico conrollers) you wanna sacrifice speed for low memory usage.

And If you are writing a software that runs on a high-end system with lots of data to process you wanna sacrifice memory usage for speed.

Let's look at an example to learn how to calculate space complexity:

```js
function sumOfFirstTheeElements(array) {
    let res = 0;    //  -- O(1)

    for (let i = 0; i < 3; i++) {   // -- O(1)
        res += array[i];
    }

    return res;
}
```

When we calculate space compexity we do not inlcude the space occupied by the inputs.

Inside our function we are only creating two variables and it does not grow as the input grows so it's constant O(1).

Let's look at another example:

```js
function generateHelloArray(n) {
    let res = [];

    for (let i = 0; i < n; i++) {
        res.push("Hello");
    }

    return res;
}
```

The input n can also be an interger, not just an array.

Here we are creating an array inside the function and the lenght of the array is same as n so the space compexity of this is O(n).

### Cheat sheet

#### The most common Big Os

**O(1)** Constant - no loops
**O(log N)** Logarithmic - usually searching algorithms have log n if they are sorted (Binary Search)
**O(n)** Linear - for loops, while loops through n items
**O(n log(n))** Log Linear - usually sorting operations
**O(n^2)** Quadratic - every element in a collection needs to be compared to ever other element. Two nested loops
**O(2^n)** Exponential - recursive algorithms that solves a problem of size N
**O(n!)** Factorial - you are adding a loop for every element

#### Rules
- Always worst case
- Remove constants
    - O(n*2) => O(n)
    - O(n+100) => O(n)
    - O(n/2) => O(n)
- Different variables for different inputs
    - O(a + b)
    - O(a * b)
- Use + sign for loops in order
- Use * for nested loops
- Iterating through half a collection is still O(n)
- Drop Non-dominant terms
    - O(n + n^2) => O(n^2)

#### What Causes Time Complexity?

- Operations (+, -, *, /)
- Comparisons (<, >, ==)
- Looping (for, while)
- Outside Function call (function())

#### What Causes Space Complexity?
- Variables
- Data Structures
- Function Call
- Allocations
