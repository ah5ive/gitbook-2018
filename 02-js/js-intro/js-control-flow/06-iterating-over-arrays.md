# Iterating Over Arrays

*After this lesson, you will be able to:*
- Iterate over an array

## What is iterating over an array?

Iterating over an array is what we call code that looks at every item in an array.
For loops are the most common way to iterate over an array. We can write for loops
in many different ways in order to find out different things about an array.

Sometimes we'll only need to look at each element in an array one at a time.
sometimes we'll need to look at two elements at a time and compare them to each other.

Some problems, like finding the minimum or maximum element in an array, require
us to store extra information in variables outside of an array as we iterate over
it.

When we're iterating over an array we need to be careful to never access an index
that doesn't exist. Arrays always start at index `0` and and at `a.length - 1`.
No negative number is ever a valid index of an array. Empty arrays have a length
of zero and we can't access any index of an empty array.

We'll show you here a collection of the most common ways to iterate over an array.

## Looking at one element at a time

This is the simplest way of iterating over an array. We write a for loop
that starts at `0` and goes while the value of `i` is less than the length
of the array.

Notice that this for loop correctly won't print anything out for an empty array.

```js
var a = [1,4,2,3,6];

for (var i = 0; i < a.length; i++) {
  console.log((a[i]);
}
```

### Exercise:
Create an `index.html` file and `script.js` file.
Run each example one at a time, .
Create a `console.log` for each interation of the array.

Make sure to format the output well so it is clear what is happening.

e.g. `console.log('iteration: '+i)` instead of `console.log(i)`.

### Further:
Investigate different ways go get values out of an array:
- what if you start `i` at different values?
- what if you change the condition to `<=`?
- what if you change the iteration?
- what if you run the loop backwards?


### Further:
Use nested for loops to iterate over this array:
```
var grid = [
  [4,5,6],
  [4,1,3],
  [7,8,2],
];
```

Write code that sums all the numbers and `console.log`s them.

Write code that sums all the numbers in one of the arrays and `console.log`s them. (i.e. `grid[0]`)

Write code that sums all the *even* numbers in one of the arrays and `console.log`s them. (i.e. `grid[0]`)

### Further:
Use nested for loops to iterate over this array:

```
var grid = [
  [
    [4,4,6],
    [4,1,3],
    [2,8,2]
  ],
  [
    [2,3,6],
    [1,1,3],
    [1,5,2]
  ],
  [
    [4,7,7],
    [1,1,3],
    [1,1,2]
  ]
];
```

Write code that sums all the numbers and `console.log`s them.

Write code that sums all the numbers in one of the arrays and `console.log`s them. (i.e. `grid[0]`)

### Further
Investigate the other iteration patterns below. Run them to see how they work.


## Other Array Iteration Patterns:

### Fencepost Problems

Sometimes we need to do special things at the beginning or end of when we're
iterating over an array.

Imagine a fence. A fence looks like this: `|=|=|=|=|'. This fence has five
fence posts and four, uh, pieces of fence.

There's a discrepency there! If we were writing a for loop to build a fence should
it run five times to place each fence post, or should it run four times to place
each piece of fence?

Consider this psuedo code that tries to place four pieces of fence:

```js
for (var i = 0; i < 4; i++) {
  placeFence();
  placePost();
}
```

The output of this code would build a fence like this: `=|=|=|=|`. There are
correctly four pieces of fence, but we're missing a fence post at the beginning!

If we switch the order of calling the `placeFence` and `placePost` methods then
we end up missing a fence post at the end of the fence.

```js
for (var i = 0; i < 4; i++) {
  placePost();
  placeFence();
}
```

This code produces a fence like this: `|=|=|=|=` without the last fence post at
the end.

The proper way to deal with a "fence post" scenario is to place one post before
or after the for loop.


```js
placePost();
for (var i = 0; i < 4; i++) {
  placeFence();
  placePost();
}
```

This code properly produces a fence with posts on each end, and fence pieces
between each post, like this: `|=|=|=|=|`.

### A Classic Fence Post Problem

The following code prints out each of the integers with a comma between each item. If the array is empty,
it should print nothing. If there is only one item in the array the function should just print the one item without any commas, like
this `42`. An array with more items should be printed like this: `42,12,97,8'.

Try to code this on your own before looking at the solution.

```js

  var a = [3,4,5,6,1,2];

  // Deal with the fence post by printing the first item in the array
  // without a comma and only when we're it is a non-empty array!
  if (a.length > 0) {
    console.log(a[0]);
  }

  // Deal with each piece of the fence by printing a comma, then the
  // value of the array at each index. Start the for loop at `i = 1`
  // to account for the fact that the first item was already printed.
  for (var i = 1; i < a.length; i++) {
    console.log("," + a[i]);
  }

  // Include an empty statement at the end to make the output
  // produce a newline.
  console.log("-");
```

You may find it more natural to deal with the fence post after the for loop.
You can do this too.

```js

  var a = [3,4,5,6,1,2];

  // Don't print anything when the array is empty. Simply return to exit
  // the function.
  if (a.length === 0) {
    return;
  }

  // Start i at zero and print each element in the array followed by a comma.
  // Set the for loop to end before `a.length - 1` to leave one element left
  // for the fence post at the end after the for loop.
  for (var i = 0; i < a.length - 1; i++) {
    console.log(a[i] + ",");
  }

  // Print the final element at the end of the list without a comma.
  console.log(a[a.length - 1]);
```

### One-Way Gates

Write code that uses an array of integers and outputs the
largest value in the array.

This problem requires us to create varaibles to store extra information outside
the for loop. We'll use if statements inside the for loop to update these variables
when certain conditions are met.

```js
  var a = [3,4,5,6,1,2];
  var largest = 0;

  for (var i = 0; i < a.length; i++) {
    if (a[i] > largest) {
      largest = a[i];
    }
  }

  console.log( largest );
```

Notice that we initialize `largest` outside of the for loop and output it at the
end. We compare each value in the array to the value and rewrite
the value of `largest` if we ever see something in the array larger than it.

There's a problem with initlializing `largest` to zero. Imagine passing an array
of negative numbers to this function. If the largest number in the collection
were `-12` this function would incorrectly return zero!

## String Builders

Some problems require building up a final result. A Classic example is traversing over
a string backwards to produce a reversed string.

Set up a variable outside the for loop to keep track of the final result.

```js
  var result = "";

  for (var i = s.length(); i >= 0; i--) {
    result += s.charAt(i);
  }

  console.log( result );
```

### Reversing an Array
The same idea can be applied to reverse an array. Create a new empty array
and push elements into it.

```
  var result = [];

  for (var i = a.length - 1; i >= 0; i--) {
    result.push(a[i]);
  }

  console.log( result );
```

### Counting One Item in an Array

Write a function called `inventory` that accepts an array of strings representing
a store inventory and accepts a string representing a product. Return the total
number of times the product occurs in the array.

```js
  var tally = 0;

  for (var i = 0; i < inventory.length; i++) {
    if (inventory[i] === product) {
      tally++;
    }
  }

  console.log( tally );
```

### Double For Loops / steed For Loops

Sometimes it's useful to nest a for loop inside a for loop. This code tests to
see if an array contains unique elements by comparing each item in the array
to every other item.

Use another variable name other than `i` for the second for loop. `i, j, k, n`
are common for loop variable names.

```js

  // look in every index
  for (var i = 0; i < a.length; i++) {

    // compare this index against every other index
    for (var j = 0; j < a.length; j++) {

      // do the comparison
      if (j !== i) {

        if (a[i] === a[j]) {
          console.log("double!: "+a[i]);
        }
      }
    }
  }
```

