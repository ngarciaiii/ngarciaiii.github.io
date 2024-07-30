---
layout: post
title:  "Record Collection"
date:   2016-09-11 18:07:30 -0400
categories: Programming
tags: [javascript]
years: ['2016']
comments: true
---
<!-- 
This problem is really interesting and fun. I have worked on it for <strong>DAYS</strong>. On the first day, I thought I solved it and got few red circles with x in them. I should have saved those <strong>TRIED SOLUTIONS</strong>. I've tried so <strong>MANY DIFFERENT APPROACHES</strong> that I forgot what they were. A day passed by, and another day of trying came and went. Every time when I thought I got it and then I crtl-enter'd to run the test. <strong>REJECTED</strong> my solutions and left me <strong>DEJECTED.</strong> <br>

Sometimes there would be few <strong>x'd red circles</strong>, and sometimes there would be one <strong>x'd red circle</strong> and hindered me from going forward to the next problem. <strong>I finally gave in. I decided to google the solution to this problem.</strong> To my amazement... there were many "solutions" online to this specific problem. <strong>More than five different solutions </strong> and they <strong>all promised</strong> to be working and will successfully progress into the next problem. <strong>Some of them even looked like mine</strong>, and I wondered where I might have gone wrong or is it some kind of a bug? So with <strong>no dignity</strong> I <strong>copied and pasted</strong> them into FCC. They got rejected! None of them worked when they promised to work. Well I found <strong>two solutions that worked out so far.</strong><br>

I found the solution on FCC's github. <strong>There wasn't any another solution ONLINE.</strong> Another solution was my close friend from college which you can follow her on [briennakh.github.io][briennakh]. She graduated from an university with Summa Cum Laude. She is a self taught programmer and a hardcore at it. Why did their solutions worked while most of other solutions promised to and failed? Apparently FCC had updated to prevent people from bypassing the problem without putting properties into an array. -->

# The problem lies below:

```javascript

// Setup
var collection = {
    "2548": {
      "album": "Slippery When Wet",
      "artist": "Bon Jovi",
      "tracks": [
        "Let It Rock",
        "You Give Love a Bad Name"
      ]
    },
    "2468": {
      "album": "1999",
      "artist": "Prince",
      "tracks": [
        "1999",
        "Little Red Corvette"
      ]
    },
    "1245": {
      "artist": "Robert Palmer",
      "tracks": [ ]
    },
    "5439": {
      "album": "ABBA Gold"
    }
};
// Keep a copy of the collection for tests
var collectionCopy = JSON.parse(JSON.stringify(collection));

// Only change code below this line
function updateRecords(id, prop, value) {


  return collection;
}

// Alter values below to test your code
updateRecords(5439, "artist", "ABBA");
```

# and the challenge is:


- Write a function which takes an album's id (like 2548), a property prop (like "artist" or "tracks"), and a value (like "Addicted to Love") to modify the data in this collection.

- If prop isn't "tracks" and value isn't empty (""), update or set the value for that record album's property.

- Your function must always return the entire collection object.

<strong>- If prop is "tracks" but the album doesn't have a "tracks" property, create an empty array before adding the new value to the album's corresponding property.</strong>

<strong>- If prop is "tracks" and value isn't empty (""), push the value onto the end of the album's existing tracks array.</strong>

- If value is empty (""), delete the given prop property from the album.


# The obstacle:

The two bold challenges above are what the most people including me failed to comply. Seems like we could success to perform either one, or another. Just not both at the same time, so if there are third or different solution that succeed <strong>please do share</strong>. Here are two different solutions below that I have found to this problem.

# Two solutions so far:

 FCC Solution which can be explained further on [freecodecamp-github][freecodecamp-recordcollection]:

``` javascript
function updateRecords(id, prop, value) {
  if (prop === "tracks" && value !== "") {
   if(collection[id][prop]) {
    collection[id][prop].push(value);
   }
   else {
    collection[id][prop]=[value];
   }
  } else if (value !== "") {
    collection[id][prop] = value;
  } else {
    delete collection[id][prop];
  }

  return collection;
}
```
<br>

Another solution could be found in [briennakh-github][briennakh]:

``` javascript
function updateRecords(id, prop, value) {
  // Add property if it doesn't exist
  if (!collection[id][prop]) {
    if (prop == "tracks") {
      collection[id][prop] = [];
    } else {
      collection[id][prop] = "";
    }
  }

  // Add value to property
  if (value) {
      if (collection[id][prop].constructor == Array) {
        collection[id][prop].push(value);
      } else {
        collection[id][prop] = value;
      }
    // Delete given prop if value is empty
    } else {
      delete collection[id][prop];
    }

  return collection;
}
```
<br>

[Update] A third solution found on [revisualize-github][revisualize]:

```javascript
function updateRecords(id, prop, value) {
  if (value !== '') {
      if (prop === 'tracks') {
          if (!collection[id].hasOwnProperty(prop)) {
            collection[id][prop] = [];
          }
          collection[id][prop].push(value);
      } else {
          collection[id][prop] = value;
      }
  } else {
    delete collection[id][prop];
  }
  return collection;
}
```



[briennakh]: https://briennakh.github.io
[freecodecamp-recordcollection]: https://github.com/FreeCodeCamp/FreeCodeCamp/wiki/Challenge-Record-Collection
[revisualize]: https://github.com/revisualize/FreeCodeCamp_Lessons/blob/master/Record_Collection.js
