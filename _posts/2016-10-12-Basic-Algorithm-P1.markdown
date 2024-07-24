---
layout: post
title:  "Basic Algorithm P1"
date:   2016-10-12 2:01:30 -0400
categories: javascript
tags: [FreeCodeCamp]
years: ['2016']
comments: true
---

After moving past Basic JavaScript and Object-Oriented Programming (OOP) parts in FCC, the fun part is Basic Algorithm. I have completed half of it so far. I am going to review each completed challenges. They should be brief and easy to understand.

# Reverse a String

- Reverse the provided string
- May need to turn the string into an array
- Result must be a string

```javascript
function reverseString(str) {
  var arraized = str.split("");
  var backward = arraized.reverse("");
  var nuStr = backward.join("");
  return nuStr;
}

reverseString("hello");
// 'olleh'
```

What I did was following the suggestions in FreeCodeCamp. Using `.split("")` to turn `str` into an array, and then no brainer, using `.reverse()` to turn array backward. Finally I used `.join("")` to turn array back into a string again. It is important to assign each function with a variable. A shortcut could be done like this below:

```javascript
function reverseString(str) {
  var reversed = str.split("").reverse("").join("");
  return reversed;
}

reverseString("hello");
// 'olleh'
```
<br>

# Factorialize a Number

- Return the factorial of provided integer
- If the integer is represented with the letter n, a factorial is the product of all positive integers less than or equal to n
- Factorials are often represented with the shorthand notation "n!"

For example: `5! = 1 * 2 * 3 * 4 * 5 = 120`

<strong>Challenge</strong>

```javascript
function factorialize(num) {
  return num;
}

factorialize(5);
```
It might be challenging at first, if out of touch with math. The `for` loop is a great way of pulling numbers magically out of a number or `num` by using indexes `i`. We want to multiply all indexes `i` from top down to one. So why not do the `for` loop backward? We will need to assign a variable to get final result. `product` came to my mind since it is mathematic. Let's set `var product = 1`. The `product` will multiply `i` and becomes the new `product` every times the loop goes through until it hits the bottom.

```javascript
function factorialize(num) {
  var product = 1;
  for (var i = num; i > 0; i--) {
    product *= i;
  }
  return product;
}

factorialize(5);
// 120
```
<br>

# Palindrome

- Return `true` if the given string is a palindrome. Otherwise, return `false`
- A palindrome is a word or sentence that's spelled the same way both forward and backward, ignoring punctuation, case, and spacing
- We'll also pass strings with special symbols, such as "2A3*3a2", "2A3 3a2", and "2_A3*3#A2"
- Given hints: use `.replace()` and `.toLowerCase()`

```javascript

function palindrome(str) {
  // Good luck!
  return true;
}

palindrome("_eye");
```
Woo... okay in this problem, I had spent awhile. Need to ignore special characters, and lowcase all letters. The first part was bit hard, but the second part is easy. I kept on testing how to use `.replace()` with `console.log()` to make sure it functions correctly.

In `.replace()` I used regular expression (regex) to either remove value, and or replace value with a new value. `.replace()` has two parameters, could use only one parameter if wanted to. `.replace(searchValue, newValue)`, so I am going to apply regex in searchValue. Regex is little confusing and weird, it is recommended to search through [stackoverflow][stackoverflow] to match your desire. `[a-zA-Z0-9_*])` includes all alphanumeric characters, underscore, and asterisk, but there is another way and is better which lays out like this `/[\W_]/`. Captialized `W` means any non-word character and important to add an underscore to it too. `[]` to include everything inside, `/.../` for start and ends, and `\` to escape. Don't forget to apply a new variable, I am going to name the variable `clean`. Test with `.console.log(clean)`.

```javascript

function palindrome(str) {
  var clean = str.replace(/[\W_]/g, '');
  console.log(clean);
}

palindrome("_eye");
// eye
```

Notice `g` at the end of the regex, it stands for global search, or search for ALL occurences. I added space for `.replace()` second parameter as a newValue. Special characters are now out of the way. Next step is pretty easy. Just type in `.toLowerCase()`. String will turn into lowcases automatically, apply new varaible to it, I am calling it `strLo`.

The third step is going to require some brain work. How am I going to have the computer to return `true` if the word is palindrome? Conditional statement is encouraged since it is a boolean. Palindrome means the first half of the word has to match with the second half of word in mirror manner looking at each letters. I am going to use the `for` loop to scrutinize each letter, and word only needs to be half so I will divide the `.length` by half.

```javascript

function palindrome(str) {
  var clean = str.replace(/[\W_]/g, '');
  var strLo = clean.toLowerCase();
  for (var i = 0; i < strLo.length/2; i++) {
  }
}

palindrome("_eye");

```
How do I determine if letter at first index matches with the letter at last index and so on looping inwardly toward fowardly or backwardly to the half of the word? The `for` loop is set. Since palindrome focues on element, I am going to put it like this `strLo[i]`. Looping through string backward has to use `strLo.length -1 - i` but adding `[ ]` to fetch elements instead of indexes. It will be easier to say if it doesn't match, then return `false` first.

```javascript

function palindrome(str) {
  var clean = str.replace(/[\W_]/g, '');
  var strLo = clean.toLowerCase();
  for (var i = 0; i < strLo.length/2; i++) {
    if (strLo[i] !== strLo[strLo.length-1-i]) {
      return false;
    }
  } return true;
}

palindrome("_eye");
// eye
```

It is important to set return `true` outside of the loop so that it inspects all letters. We will continue with Basic Algorithm Part 2, 3, and 4 in different posts.

[stackoverflow]: https://stackoverflow.com
