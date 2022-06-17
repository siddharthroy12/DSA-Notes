# My notes on DSA and leetcode questions

## Table of Contents
1. [Big O](#big-o)

## Big O

The Big O notation is used to show how well an algorithm scales in terms of speed and space as the input grows.
It indicates how much time and memory an algorithm will take to solve an problem for a given input.

Because a code can run faster or slower on different processors it's not a good way to calculate the efficency of a program. That's why we use Big O notation to show how well a code performs when the input grows.

Big O can also be plotted to a graph:

![Big O Graph](./Big-O-Graph.png)

### To caculate Big O

To calculate Big O we need to calculate how many operations the code/function/program will take for the given input.

For example this code:

```js
function getFirstElement(array) {
    return array[0];    // -- O(1)
}
```

This code returns the first element of an array so it has only one operation so the Big O of this function
is O(1).

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
So in the best case if the element is at the first index it will only do one operation O(1) but in the worst
case the number of operations will be equal to the number of inputs which it denoted by O(n).

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

You might think that the Big O of this function is O(n) + O(3) = O(n+3). But we don't count the constant numbers like 3 because what if the number of elements is 1000 then having extra 3 operation doesn't matter to us, so we remove the constant and this becomes O(n).

> In big tech we often work with big amount of data


But what if we have two for loops?

```js
function getSumAndMultipleOfElements(array) {
    let sum = 0;
    let multiple = 0;
    
    for (let i = 0; i < 3; i++) {   // -- O(N)
        sum += array[i];
    }

    for (let i = 0; i < 3; i++) {   // -- O(N)
        multiple *= array[i];
    }

    return { sum, multiple };
}
```

We have to O(n) here so it should become O(2n) right?
Even though the graph of this is steeper than O(n) it's still a straight line (a linear graph), so once again we remove the constant and it becomes O(n).

For nested for loops: