---
layout: post
title:  "Basic Algorithm P2"
date:   2016-10-16 8:05:30 -0400
categories: Programming
tags: [javascript]
years: ['2016']
comments: true 
---

The fun and challenging part of FCC continues, Basic Algorithm Part 2.

# Find the Longest Word in a String

- Return the length of the longest word in the provided sentence
- Your response should be a number
- Given hints: use `.split()` and `.length`

<strong>Challenge</strong>

```javascript
function findLongestWord(str) {
  return str.length;
}

findLongestWord("The quick brown fox jumped over the lazy dog");
```

The problem with a string is that it is immutable. `.split(" ")` is going to turn a string `str` into an array `arr`. Adding space in between the quotes is important, because I would like for the string to be split into per a word, and not into per a character or into letters. Use `for` loop to go through each word, and to get number of characters in each word would need a `.length`.

```javascript
function findLongestWord(str) {
  var arr = str.split(" ");
  for (var i = 0; i < arr.length; i++) {
  }
  return str.length;
}

findLongestWord("The quick brown fox jumped over the lazy dog");
```

Now `i` short for my "index" will loop through each word in an array `arr`, and what I want to do is put down a code that will count the number of indexes in element. My goal is to keep the biggest word, while bypass smaller words. I am going to create a variabe `biggest` and set it to `0`. Whenever word's bigger than the `biggest`, set that word to `biggest`.

```javascript
function findLongestWord(str) {
  var arr = str.split(" ");
  var biggest = 0;
  for (var i = 0; i < arr.length; i++) {
    if (arr[i].length > biggest) {
      biggest = arr[i].length;
    }
  }
  return biggest;
}

findLongestWord("The quick brown fox jumped over the lazy dog");
// 6
```
<br>

# Title Case a Sentence

- Return the provided string with the first letter of each word capitalized. Make sure the rest of the word is in lower case
- For the purpose of this exercise, you should also capitalize connecting words like "the" and "of"
- Given hint: use `.split()`

```javascript
function titleCase(str) {
  return str;
}

titleCase("I'm a little tea pot");
```
I am supposed to aim for `// I'm A Little Tea Pot`. Programming, I would think, is like being a chef, gotta to do a food prep before I cook up ingredients altogether to make it taste great. I am going to `toLowerCase()` and `.split()` the string at the same time to lowercase everything and arraize it a new varaible `strLoAr`. A `for` loop to go through each word with an `i` is needed. One more `for` loop for a letter in word using `j`, an index within an index/element. Let's set up a prep right now.  

```javascript
function titleCase(str) {
  var strLoAr = str.toLowerCase().split(" ");
  for (var i = 0; i < strLoAr.length; i++) {
    for (var j = 0; j < strLoAr[i].length; j++) {
    }
  }
  return str;
}

titleCase("I'm a little tea pot");
```
Okay, now let's replace first letter of each word with a capitalized letter. In order to capture the first letter and manipulate it, is using a conditional statement `if (j === 0)` in second `for` loop. I am going to remove the first letter by using `.slice()` and rename the remaining `strLoAr` to a new variable `fixed`. Extract the first letter from each word in a former array `strLoAr`, and captialize it and then put into a new variable `capped`. I realized that I would need a new empty array, so I created and named it `titled` to apply `.push()`. I want to add `capped` to `fixed` in `titled`. Always check each new variable with a `console.log()` to ensure it comes as desired.

```javascript
function titleCase(str) {
  var strLoAr= str.toLowerCase().split(" ");
  var capped;
  var fixed;
  var titled = [];
  for (var i = 0; i < strLoAr.length; i++) {
    for (var j = 0; j < strLoAr[i].length; j++) {
      if (j === 0) {
        fixed = strLoAr[i].slice(1);
        capped = strLoAr[i][j].toUpperCase();
      }
    } titled.push(capped + fixed);
  } return titled.join(" ");
}

titleCase("I'm a little tea pot");

// 'I\'m A Little Tea Pot'
```

In some consoles like [repl.it][repl.it], it will show backslash in "I'\m" but it won't render.
<br>

# Return Largest Numbers in Arrays

- Return an array consisting of the largest number from each provided sub-array
- For simplicity, the provided array will contain exactly 4 sub-arrays
- Remember you can iterate through an array with a simple for loop, and access each member with array syntax `arr[i]`
- Should return an array
- Given Hint: Comparison Operators

```javascript
function largestOfFour(arr) {
  return arr;
}

largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]);
```

Outline below every challenge is usually directly copied and pasted from [freecodecamp][fcc], and it suggested me to use `arr[i]`. Of course I am going to use a `for` loop to iterate through arrays. I came up with two different solutions. First one was easy and I felt like I cheated. If it works, then it isn't a cheat, but would be better to learn how to do the long way. I am going to put down the first solution and explain quickly. I used `Math.max` to solve the problem.

```javascript
function largestOfFour(arr) {
  var tallest= [];
  var max;
  for (var i = 0; i < arr.length; i++) {
    max = Math.max.apply(null, arr[i]);
    tallest.push(max);
  } return tallest;
}

largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]);
// [ 5, 27, 39, 1001 ]
```
I set a new array named `tallest`. I processed to create a `for` loop. I looked through [stackoverflow][sof] on how to use Math.max and it suggested me to use `.apply()`. I decided that I would use a new variable `max` to make it easier. So I set `max` to `Math.max.apply(null, arr[i])` inside `for` loop and then push it into array `tallest`. Return `tallest` outside of `for` loop to allow loop to complete. `null` is an intentional absence of any object value, allowing computer to ignore completely, or bypass. `.apply(thisArg, [argsArray])` is the default and I am using `Math.max` as a function so I used `null`. That was the quick way.

Let's do the long way. Setting a new empty array `tallest` since there are four different arrays and I want to pluck largest number out of each, and put them into one array. First `for` loop to iterate through an array with arrays inside. Recall the challenge on the top of this page, "Find the Longest Word", it is almost the same idea. I created a new variable `max` to hold the biggest number in. I set `max` to `0`. Second `for` loop to iterate through indexes/[element]s in each array. if an element `arr[i][j]` is bigger than `max`, set it to `max`. Outside the second `for` loop, push it into `tallest` array. outside both loops, return `tallest`.

```javascript
function largestOfFour(arr) {
  var tallest = [];
  for (var i = 0; i < arr.length; i++) {
    var max = 0;
    for (var j = 0; j < arr[i].length; j++) {
    if (arr[i][j] > max){
      max = arr[i][j];
    }
  } tallest.push(max);
  } return tallest;
}

largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]);
// [ 5, 27, 39, 1001 ]
```

[repl.it]: https://repl.it
[fcc]: https://freecodecamp.com
[sof]: https://stackoverflow.com
