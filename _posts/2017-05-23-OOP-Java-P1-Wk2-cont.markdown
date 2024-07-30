---
layout: post
title:  "OOP Java P1 Wk2 cont."
date:   2017-05-23 10:07:30
categories: Programming
tags: [java]
years: ['2017']
comments: true
---

### NOTE:
I used [Eclipse][Eclipse] for week2, until realized had to use [Netbeans][Netbeans] to release third week exercises. I transferred codes from Eclipse to Netbeans. It's recommended to use Netbeans for [MOOC][MOOC].

# The 2nd part of the Week 2!

The first part of the Week 2 is all about looping and using basic mathematics. Now this second part of the Week 2 is going to be about using looping and basic mathematics on strings. Plus we will get to learn how to do methods properly!

# EXERCISE #37 & #38

In this exercise, it enables us to <strong>understand how method works</strong>. We create a method then apply to the <strong>main</strong> method. <strong>Method is pretty much a function...</strong> well it can be used as a field attribute, but mostly used as a function. Take a look below!

```java
package week2;

import java.util.Scanner;

public class week2_ex37_38{
    public static void main(String[] args) {
        Scanner reader = new Scanner(System.in);

        System.out.print("How many? ");
        int i = 0;
        int num = Integer.parseInt(reader.nextLine());
        num = num - 1;

        while( i <= num) {
            printText();
            i++;
        }
    }

    public static void printText(){
        System.out.println("In the beginning there were the swamp, the hoe, and Java");
    }
}
```

The assignment is to create a method `printText()` that only prints a string. A very simple and cute method. That is the exercise #37. It isn't the end of that exercise, I am to include method `printText()` inside the `main(String[] args)` method. It shows me that the "inside" method pops out its function in the `main()` method. It only can be done that way. <strong>Class file must have a main method, because it is the entry point to execute functions out.</strong> If a package has mutilple class files, can use just one class file's main method to execute (don't worry about that now).

In <strong>Exercise #38</strong>, it wants me to carry out `printText()` mutiple times at the number of user's preference. <strong>Since `main()` method is the only executable method</strong>, add the `while()` loop inside `main()` method. We know how to do loop with an increment, no need to explain how, or go back to previous post. Insert `printText()` inside the loop in `main()`. Da-ta! The method is executed.

# EXERCISE #30 & #40

This exercise will teach more about methods involving with printing stars and them into shapes! Exciting, isn't it?

Let's do a simple programming...
- create a method that prints star and allow user to decide how many stars should be printed

```java
public static void printStars(int amount){
    int i = 0;
    while (i < amount) {
        system.out.print("*");
        i++;
    } system.out.println();
}

public static void main(String[] args) {
    printStars(5);
    printStars(3);
    printStars(9);
}

// Result:
// *****
// ***
// *********
```

A real simple programming, now let's do all other bits of this <strong>Exercise #39</strong> altogether! I am going to be doing several methods. The list below are methods it wants me to create:

- printing stars into a shape square aka method `printSquare(int sideSize)`
- printing stars into a rectangle aka method `printRectangle(int width, int height)`
- printing stars into a left-aligned triangle aka method `printTriangle(int size)`

```java
public class Printing {

    public static void printStars(int amount) {
        // 39.1
        int i = 0;
        while(i < amount) {
            System.out.print("*");                          
            i++;
        } System.out.println();
    }

    public static void printSquare(int sideSize) {
        // 39.2
        int i = 0;
        while (i < sideSize) {
            printStars(sideSize);
            i++;
        } System.out.println();
    }

    public static void printRectangle(int width, int height) {
        // 39.3
        int i = 0;
        while (i < height) {
            printStars(width);
            i++;
        } System.out.println();
    }

    public static void printTriangle(int size) {
        int i = 1;
        while (i <= size) {
            printStars(i);
            i++;
        }
    }

    public static void main(String[] args) {
        printStars(3);
        System.out.println("\n---");
        printSquare(4);
        System.out.println("\n---");
        printRectangle(5, 6);
        System.out.println("\n---");
        printTriangle(3);
        System.out.println("\n---");
    }

}
```

Each method does a task, but is not executed until it's in method `main()`. I think it's better to split tasks into methods and then put altogether under one method. This is very basic. We will get a better understanding on "methods" in next post <strong>Guessing A Number</strong>. Let's go over to <strong>Exercise #40</strong>, similar with <strong>Exercise #39</strong>. I might need to cover one method that is kind of troublesome.

What <strong>Exercise #40</strong> asks for:

- create a method `printWhitespaces(int size)`, giving amount of whitespaces
- create a method `printTriangle(int size)`, this time right-aligned
- create a christmas tree using all previous methods

The top is easy to do, just use `printStars` method from <strong>Exercise #39</strong> and replace star with a whitespace " ". Be sure to take `System.out.println();` off!

Now this method `printTriangle()` right-aligned is where I got stuck for a bit. <i>Oui</i> rusty. Take a look:

```java
public static void printTriangle(int size) {
    int i = 1;
    while(i <= size) {
        printWhitespaces(size - i);
        printStars(i);
        i++;
    }
}

//    *
//   **
//  ***
// ****

```

How do I make a right-aligned triangle? Earlier, this exercise asked me to create a `printWhitespaces()`, so that's a hint. Adding `printWhitespaces()` method inside this method. Let's say if `size` is given a `4` and it goes in both `printStars(size)` and to `printWhitespaces(size)`.  Basically, there's <strong>4 characters</strong> made of <strong>either stars, or whitespaces</strong>. There will be 4 stars on the bottom for sure, and there won't be any whitespace. Now about top, we want one star on top, and meaning need three whitespaces. We have no problem printing desired number of star/s, but how do we make whitespaces come first? Place `printWhitespaces()` first inside the loop. We want three whitespaces and `size` in this case means 4 characters. 4 characters - 1 star = 3 whitespaces. Ah-ha! `printWhitespaces(size-1);`

Loop rolls on, `size` reduce its number, but still subtracting `1` inside `printWhitespaces()`, giving the right amount of whitespaces needed. `printStars()` method on the next, creating right-aligned triangle.

<strong>xmasTree(int height) Method</strong>

The last part of this <strong>Exercise #40</strong> wants me to create a xmas tree using all previous methods, and maybe small tweaks. Don't worry about xmas trunk or the bottom part. <strong>The challenge is making right-aligned triangle and left-aligned triangle go together.... or is it?</strong>

Using `printWhitespaces()` and `printStars()` again and this time `height` as an argument. `printWhitespaces()` placed first in the loop and subtracts by 1 same as with right-aligned triangle method. Now next step is the tricky part. It might look like left-aligned triangle and right-aligned triangle is thrown together to make a xmas tree. <strong>Actually it isn't!</strong>

```java
public static void xmasTree(int height) {
int i = 1;
    while (i <= height) {
        printWhitespaces(height - i);
        printStars(2 * i - 1);
        i++;
    }
}
```

Insert `printStars()` beneath `printWhitepsaces()`. If `height` is appointed to a number `4`, for xmas tree, we want one star on the top always. On the second row, we wouldn't want two stars because top star wouldn't be in the middle above two stars. We will need three stars on the second row.

- each row should have odd numbers of stars
- able to manipuate the number of stars in `printStars()` through each loop
- `printWhitespaces()`'s true function is to make a slope angle
- `printStars()`'s true function is to print a number of stars

<strong>The trick</strong>

we used modulo `% 2 = 0` to find even number. Well we could multiply by 2 to make <strong>any number</strong> an even number too. <strong>2 is a magical number!</strong> But if we substract the product by 1, it will always be an odd number. We will use `i` to manipulate `printStars()`.

if height = 4

`printStars(2 * i - 1 );` = 2 * 1 - 1 = 1 star     
`printStars(2 * i - 1 );` = 2 * 2 - 1 = 3 stars     
`printStars(2 * i - 1 );` = 2 * 3 - 1 = 5 stars    
`printStars(2 * i - 1 );` = 2 * 4 - 1 = 7 stars    

See how that works?

If printed, we get a triangle. Stumped, not a xmas tree. Time to make a stump!

I at first thought stump was going to be easy to create, since it's just a square or rectangle... oops! Forgot about whitespaces, how to keep stump in the middle. What if user decided to give xmasTree(height) a height of 10 or 20? Let's try again.  

We want to manipualate `printWhitespaces()` based on `xmasTree()`. Stump only needed to be 2 stars tall. We could use `i` again, because the first `while()` loop is completed, and then second `while()` loop may continue. So set `i` to 2 and have it decrements down to 0. How do we manipulate `printWhitespaces()` according to `xmasTree()`'s `height`?  

```java
i = 2;      
while (--i >= 0) {
    printWhitespaces(height - 2);
    printStars(3);
}
```

Yep! Using `height` to correlate with `printWhitespaces()`. Stump will always be aligned in the middle based on it height. All small tasks are turned into methods, and thrown altogether into `main()` method to make it work. That's fantastic!

```java
public static void xmasTree(int height) {
    int i = 1;
    while (i <= height) {
        printWhitespaces(height - i);
        printStars(2 * i - 1);
        i++;
    }

    i = 2;      
    while (--i >= 0) {
    printWhitespaces(height - 2);
    printStars(3);
    }
}

public static void main(String[] args) {
    System.out.println("---");
    xmasTree(4);
    System.out.println("---");
    xmasTree(10);
}
```


[NetBeans]: https://www.netbeans.org
[Eclipse]: http://www.eclipse.org/downloads/packages/
[MOOC]: https://www.mooc.fi/
