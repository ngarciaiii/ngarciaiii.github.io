---
layout: post
title:  "Guessing A Number"
date:   2017-05-25 05:56:30
categories: Programming
tags: [java]
years: ['2017']
comments: true
---


I used [Eclipse][Eclipse] until I realized that I needed to use [NetBeans][NetBeans] to unlock [MOOC.FI][MOOC.FI]'s upcoming week exercises. NetBeans has components and methods ready to use whereas I had to make my own methods in Eclipse.

This is <strong>Week 2 Exercise #41</strong>. I did every exercises in Eclipse until end of Week 2 including this one. This exercise to me is mostly about creating methods and applying them. My Eclipse codes won't pass in NetBeans, but I feel that my codes in Eclipse give a <strong>better idea of what methods are</strong>.

Listing out all the bits of this exercise on what we are to do.

- create `drawNumber` method that generates a random number between 0 and 100
- have an user to guess a number
- let user know that number is either lesser or greater and or user guessed right!
- Let user repeat guesses while `drawNumber` stays the same
- print the number of guesses attempted along with the answer


I didn't come up with this code on my own. I used [stackoverflow][stackoverflow]. This is the way to generate a random number. Setting that `drawNumber()` method. The drawn number is set to varible `num`. Notice how I put down `int` after `public static` instead of `void`. Remember `void` means no returned value. In this method, we are returning a drawn number. so it's an `int`.

```java    
// Generates random number
public static int drawNumber() {
    int num =(int)(Math.random() * 100 + 1);
    System.out.println(num);
    return num;
}
```

The next step is creating a method `guess()` that has reader reading user's guess. Again, user is guessing a number and this will return an integer value. I am putting down `int` instead of `void`. The guess is returned as `guess`.

```java
// Read user's guess
public static int guess() {
    Scanner reader = new Scanner(System.in);
    System.out.print("Guess a number: ");
    int guess = Integer.parseInt(reader.nextLine());
    return guess;
}
```

The third step is notifying user whether his/her guess is right. If not then let him/her know that the guessing number is either greater, or lesser. Isn't that like a boolean? Let's do this in boolean fashion. I am putting down `boolean` instead of `void`. Thanks to [briennakh][briennakh], that was her idea. I am going to name this method `checkGuess(int guess, int num)`. Using same varibles and values from two other methods above. It is important to repeat what type of values or varibles they are. Java is static.

```java
// Check guess against given number
public static boolean checkGuess(int guess, int num) {
    if (guess == num) {
        System.out.println("You have guessed it!");
        return true;
    } else if (guess > num) {
        System.out.println("The guessing number is greater.");
        return false;
    } else {
        System.out.println("The guessing number is lesser.");
        return false;
    }
}
```

<strong>Time to make the main method!</strong> The first step inside the method is draw the number. That's how Guess A Number game starts. Again, repeat the type of value or variable. `int num = drawNumber();` and the number is drawn. I added `System.out.println(num);` because I want to make sure `drawNumber()` works. Could do that inside `drawNumber()` method, but why not here too. Could remove them after knowing that they do work! I am going to lay them out now and add other perks.

```java
// Run program
public static void main(String[] args){
    int num = drawNumber();
    System.out.println(num);
    System.out.println();
    int guesses = 5;
    while(guesses > 0) {
        int guess = guess();
        boolean correct = checkGuess(guess, num);
        if (correct) {
            break;
        }

        guesses--;
        System.out.println("You have " + guesses + " guesses left");
        System.out.println("Try again!");
        System.out.println();
    }
}
```

I want to limit the number of guesses to 5. Note `guess` and `guesses` are two different things. `guess` is the value of user's guessing number. `guesses` is the number of how many guessing attempts user had made. `int guess` is the input given from `guess()` by a user. Notice how guess has an type defined by `int`. That's Java. I am going to add `boolean` for `checkGuess(guess, num)`, giving its a varible `correct` to use in a conditional statment. The loop ends in two different ways. If guesses reach down to 0, then it has expired, or if user guessed right then `break;`.

## Let's put all methods together and get an overview!

```java
package week2;

import java.util.Scanner;

public class week2_ex41{

    // Generates random number
    public static int drawNumber() {
        int num =(int )(Math.random() * 100 + 1);
        System.out.println(num);
        return num;
    }

    // Read user's guess
    public static int guess() {
        Scanner reader = new Scanner(System.in);
        System.out.print("Guess a number: ");
        int guess = Integer.parseInt(reader.nextLine());
        return guess;
    }

    // Check guess against given number
    public static boolean checkGuess(int guess, int num) {
        if (guess == num) {
            System.out.println("You have guessed it!");
            return true;
        } else if (guess > num) {
            System.out.println("The guessing number is greater.");
            return false;
        } else {
            System.out.println("The guessing number is lesser.");
            return false;
        }
    }

    // Run program
    public static void main(String[] args){
        int num = drawNumber();
        System.out.println();
        int guesses = 5;
        while(guesses > 0) {
            int guess = guess();
            boolean correct = checkGuess(guess, num);
            if (correct) {
                break;
            }

            guesses--;
            System.out.println("You have " + guesses + " guesses left");
            System.out.println("Try again!");
            System.out.println();
        }
    }
}
```

## We have a Guess A Number game!    

[NetBeans]: https://www.netbeans.org
[Eclipse]: http://www.eclipse.org/downloads/packages/
[MOOC.FI]: https://www.mooc.fi/
[stackoverflow]: https://www.stackoverflow.com
[briennakh]: https://github.com/briennakh
