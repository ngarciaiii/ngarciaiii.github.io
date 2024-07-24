---
layout: post
title:  "Profile LookUp"
date:   2016-09-17 14:23:30 -0400
categories: javascript
tags: [FreeCodeCamp]
years: ['2016']
comments: true
---
I took a look into this new challenge, and thought it was going to be easy. After few tries, I failed to realize that computer parses, and not necessarily read the same way as I do. I wasn't accessing right. I miscommunicated with the computer.

# The Challenge is:

  - Check if `firstName` is an actual contact's `firstName` and the given property (`prop`) is a property of that contact
  - If both are true, then return the "value" of that property
  - If `firstName` does not correspond to any contacts then return `"No such contact"`
  - If `prop` does not correspond to any valid properties then return `"No such property"`


```javascript
//Setup
var contacts = [
    {
        "firstName": "Akira",
        "lastName": "Laine",
        "number": "0543236543",
        "likes": ["Pizza", "Coding", "Brownie Points"]
    },
    {
       "firstName": "Harry",
       "lastName": "Potter",
       "number": "0994372684",
       "likes": ["Hogwarts", "Magic", "Hagrid"]
    },
    {
        "firstName": "Sherlock",
        "lastName": "Holmes",
        "number": "0487345643",
        "likes": ["Intriguing Cases", "Violin"]
    },
    {
        "firstName": "Kristian",
        "lastName": "Vos",
        "number": "unknown",
        "likes": ["Javascript", "Gaming", "Foxes"]
    }
];


function lookUpProfile(firstName, prop){
// Only change code below this line

// Only change code above this line
}
// Change these values to test your function
lookUpProfile("Akira", "likes");
```

The challenge sounds simple, but ah-ha, how do you loop through the nested objects in an array? FreeCodeCamp provided handful of lessons before this challenge. The lesson <strong>Iterate through an Array with a For Loop</strong> explained:

```javascript

var arr = [10,9,8,7,6];
for (var i=0; i < arr.length; i++) {
   console.log(arr[i]);
}

//--> 10, 9, 8, 7, 6
```

All I had to do to loop through an array is putting down array's name dot `length`. Sounds easy, but wait! There are many objects and many `firstName` in the array, how am I going to find the specific property `firstName` that I am looking for? Another lesson in FreeCodeCamp <strong>Accessing Nest Array</strong> gave an example using array bracket notation and index.

```javascript

var myPlants = [
  {
    type: "flowers",
    list: [
      "rose",
      "tulip",
      "dandelion"
    ]
  },
  {
    type: "trees",
    list: [
      "fir",
      "pine",
      "birch"
    ]
  }  
];

var secondTree = myPlants[1].list[1];

//--> secondTree = pine
```
However this challenge has nested objects in an array, and these are where `firstName` are located in. FCC's <strong>Accessing Nested Objects</strong> lesson teaches that nested object can be accessed by either using dot or bracket notation.

```javascript

var myStorage = {
  "car": {
    "inside": {
      "glove box": "maps",
      "passenger seat": "crumbs"
     },
    "outside": {
      "trunk": "jack"
    }
  }
};

var gloveBoxContents = myStorage.car.inside["glove box"] ;

//-->gloveBoxContents = maps
```

# Let's get to work!

We need to access into an array `contacts` and loop through nested objects until one of arguments matches with the `firstName`.

```javascript

function lookUpProfile(firstname, prop) {
    for (var i = 0; i < contacts.length; i++) {
        if (contacts[i].firstName === firstName) {
        }
    }
}

```
`i` loops through each nested objects in an array `contacts`, and until `firstName` matches. In the challenge, there are rules like if `firstName` doesn't match, and if there isn't any `prop`, would need to return why cannot complete. If `firstName` matches and has a `prop`, then return the value.

```javascript
function lookUpProfile(firstName, prop){
    for (var i = 0; i < contacts.length; i++) {
        if (contacts[i].firstName === firstName) {
            if (prop in contacts[i]) {
                return contacts[i][prop];
            } else {
                return "No such property";
            }
        }
    }
    return "No such contact";
}
```
