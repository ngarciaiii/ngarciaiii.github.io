---
layout: post
title:  "Basic JavaScript: Nesting For Loops"
date:   2016-08-21 17:23:30 -0400
categories: javascript
tags: [FreeCodeCamp]
years: ['2016']
comments: true
---

I have been learning basic javascript on freecodecamp.com, and this is the second problem that I encountered a bit difficult of understanding. It wanted me to modify function multiplyAll so that it multiplies the product variable by each number in the sub-arrays of arr.

``` javascript
function multiplyAll(arr) {
  var product = 1;
  // Only change code below this line

  // Only change code above this line
  return product;
}

// Modify values below to test your code
multiplyAll([[1,2],[3,4],[5,6,7]]);
```

# The challenge is:

<strong>Modify function multiplyAll so that it multiplies the product variable by each number in the sub-arrays of arr

- `multiplyAll([[1],[2],[3]]);` should return `6`
- `multiplyAll([[1,2],[3,4],[5,6,7]]);` should return `5040`
- `multiplyAll([[5,1],[0.2, 4, 0.5],[3, 9]]);` should return `54`


I wasn't sure how to manipulate elements inside arrays within an array. I decided to research a bit about array. There are few different types of arrays, and are exemplified below:

homogeneous arrays: stores single type of data (i.e. string, or int, or boolean) in an array

``` javascript
var array = ["Matthew", "John", "Luke"];
var array = [27, 30, 35];
var array = [true, false, true];
```                

heterogeneous array: stores mixed data types in an array

``` javascript
var array = ["Matthew", 27, true];
```


multidimensional array: an array of arrays, or array-ception like inception

``` javascript
var array = [
    ["Matthew", "27"],
    ["Simon", "24"],
    ["Luke", "30"]
];
```

jagged array like multidimensional array but not in uniformed set

``` javascript
var array = [
    ["Matthew", "27", "Developer"],
    ["Simon", "24"],
    ["Luke"]
];
```

 The problem I try to solve is multidimensional array, or 2D array since there is array in an array (2 arrays). Meaning two loops needed. I decided to play with the freecodecamp's provided example using [repl.it][repl.it] a better console to practice with.

``` javascript
var arr = [
  [1,2], [3,4], [5,6]
];
for (var i=0; i < arr.length; i++) {
  for (var j=0; j < arr[i].length; j++) {
    console.log(arr[i][j]);
  }
}

// 1, 2, 3, 4, 5, 6
// => undefined
```

What happens if I used `console.log(arr[i]);` without `j`? It will print out:

```
[ 1, 2 ]
[ 1, 2 ]
[ 3, 4 ]
[ 3, 4 ]
[ 5, 6 ]
[ 5, 6 ]
```

The invisible action is that `j` loop went through each element in the arrays, but `arr[i]` prints out its "elements" which are arrays therefore its element was printed twice because of `j` loop. If I take out `for (var j=0; j < arr[i].length; j++)`, and then it will print `arr[i]`'s elements:

```
[1, 2]
[2, 4]
[5, 6]
```

Now what happens if I used `console.log(arr[j]);` instead? It comes out:

```
[ 1, 2 ]
[ 3, 4 ]
[ 1, 2 ]
[ 3, 4 ]
[ 1, 2 ]
[ 3, 4 ]
```

Didn't even touch third array within primary array. Let's find out why by this `console.log(arr[i], i);` :

```
[ 1, 2 ] 0
[ 1, 2 ] 0
[ 3, 4 ] 1
[ 3, 4 ] 1
[ 5, 6 ] 2
[ 5, 6 ] 2
```

 Can deduce that there is a difference between `[i]` and `i`. `[i]` prints elements (secondary arrays in this case) and `i` prints its elements' indexes. Again, test with `console.log(arr[i], j);` :

```
[ 1, 2 ] 0
[ 1, 2 ] 1
[ 3, 4 ] 0
[ 3, 4 ] 1
[ 5, 6 ] 0
[ 5, 6 ] 1
```

`[i]` prints all secondary arrays. We can see that `j` prints index of each element inside secondary arrays. `[i]` loop went every secondary arrays and `j` loop went through elements in each secondary array separately. Let's try `console.log(arr[j], i);` :

```
[ 1, 2 ] 0
[ 3, 4 ] 0
[ 1, 2 ] 1
[ 3, 4 ] 1
[ 1, 2 ] 2
[ 3, 4 ] 2
```

`[j]` didn't cover third array's elements and `i` has a total of three indexes even though there isn't a third array. Why? Test this one `console.log(arr[j], j);` :

```
[ 1, 2 ] 0
[ 3, 4 ] 1
[ 1, 2 ] 0
[ 3, 4 ] 1
[ 1, 2 ] 0
[ 3, 4 ] 1
```

Almost similar result and from these results, it might be obvious because of this `j < arr[i].length;` which allowed `j` loop to go only twice since `i` is the total of three indexes.  `i` loop goes through indexes of arrays and `j` loop goes through indexes of elements.

Lastly... test `console.log(arr[j], [i]);`:

```
1
2
3
4
undefined
undefined
```

`arr[j]` only has two indexes, couldn't go through third array. `[i]` fetches the elements and print them out. <strong> Letters are not really the culprits. It is the matter of loops.</strong> First `[]` loop goes through secondary arrays, and second `[]` loop prints secondary arrays' elements out.

So what happened with `arr[i][j]`?

1) `[]` is an array symbol and focuses on elements rather than indexes. <br>
2) `[i]` loop goes through primary array's elements which are secondary arrays.<br>
3) `[j]` loop goes through and print secondary arrays' elements.


# Back to the challenge and the solution lies below:

``` javascript
function multiplyAll(arr) {
  var product = 1;

  // Only change code below this line
  for (var i = 0; i < arr.length; i++) {
    for (var j = 0; j < arr[i].length; j++) {
      product = product * arr[i][j];
    }
  }
  // Only change code above this line
  return product;
}

// Modify values below to test your code
multiplyAll([[1,2],[3,4],[5,6,7]]);
```

Now we know that `arr[i][j]` fetches all secondary arrays' elements by using two loops.

- Create `product` that equals to `1`.
- `product` follows `j` loop in `i` loop, and `arr[i][j]` fetches an element at a time.
- `product` multiples with `arr[i][j]` element then becomes the "new" `product`.
- `j` loops again and "new" `product` multiples with the next fetched element.
- `j` loop repeats until there is not any element left and leaving the final product.

[repl.it]: https://www.repl.it
