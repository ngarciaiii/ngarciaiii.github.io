---
layout: post
title:  "OOP Java Part 1 cont."
date:   2017-05-01 4:06:30
categories: Programming
tags: [java]
years: ['2017']
comments: true
---

# Continuing OOP Java Part 1

Continuing OOP Java Part 1 from University of Helsinki's [MOOC][MOOC] (Massive Open Online Courses). This post will cover <strong>week 1 #20-23</strong> exercises. Last exercise will be used in [NetBeans][NetBeans], because that exercise rely on component that is exclusively installed in NetBeans.

# Using .equals

Every programming languages have some similarities and differences. I would say that Python and JavaScript are closer to each other than to Java. Java do have some resemblances with both of these languages. This `.equals` is different from these. In Java, <strong>String</strong> cannot be compared using equality operator `==`. An example in <strong>Exercise #20</strong> shows that.

```java
package usingScanner;

import java.util.Scanner;

public class week1_ex19_21 {
	public static void main(String[] args) {
		Scanner reader = new Scanner(System.in);

		String username1 = "alex";
		String password1 = "mightyduck";

		String username2 = "emily";
		String password2 = "cat";


		System.out.print("What is your username?: ");
		String username = reader.nextLine();
		System.out.print("What is your password?: ");
		String password = reader.nextLine();


		if (username.equals(username1) && password.equals(password1)) {
			System.out.println("You are now logged in!");
		} else if (username.equals(username2) && password.equals(password2)) {
			System.out.println("You are now logged in!");
		} else {
			System.out.println("Your username or password is invalid.");
		}
```		

In that exercise, all variables created are strings. Usernames and passwords are created, and then using conditional statements to verify whether usernames and passwords match or not. `&&` is one of operators like in JavaScript, and `and` for Python; short for "true AND true" condition. `username.equals(username1) && password.equals(password1)` is a condition saying that username1 and password1 TOGETHER is true. Java's `.equals` will bite us in the butt someday later if we forget about it and for using equality operator instead. NOTE: This is not the proper way to store username and password, just a practice.

# Leap Years

<strong>Exercise #21</strong> is pretty neat and it's about using `&&`. It wants us to check if the year is a leap year or not. The rules for a year to be a leap year:

- divisible by 4
- if divisible by 100 then it has to be divisible by 400 too

There are four different years to test: 2011, 2012, 1800, 2000.

```java

  System.out.print("Enter the year: ");
  int year = Integer.parseInt(reader.nextLine());

  if (year % 4 == 0 && year % 100 == 0 && year % 400 == 0) {
    System.out.println("It is a leap year!");
  } else if (year % 4 == 0 && year % 100 != 0) {
    System.out.println("It is a leap year!");
  } else {
    System.out.println("It is NOT a leap year.");
  }

```

It took me awhile to solve this. I tried three different codings and they did not work. It's mostly about logic processes. I think this exercise is great way of showing how condition is very strict and inflexible. The first `if` statement says if year is divisible by 4, 100, and 400 then it is a leap year. It doesn't worry about year that is divisible by 4 alone. Any year that is divisible by 4 will be considered not a leap year. So add `else if` year is divisible by 4 alone and not by 100, or 400 for that matter, then it is a leap year. Important, let computer read that as a second command so that way it will look for a year that's divisible by both 4, and 100 first. `Else` means everything else, therefore is not a leap year.

# while(true)

This <strong>Exercise #23</strong> uses <strong>NetBeans</strong> because it contains a component exclusively. It has a `Graph.java` that automatically opens up a graph based on data we write in our java file. Mine is `week1-ex23.java`, name yours whatever. In this exercise, `while(true)` loop is used. If it is used in a wrong way, could trigger an infinite loop. We don't want that because it will crash our computer. The way to end a while(true) loop is to have a `break;`

It wants us to create a program that asks us to:

- input a floating point number as often as we want to
- numbers inputed need to be between -30 and 40 degree
- if it is below -30 and above 40, then have program to ignore it and not include it into the Graph

`while(true)` will repeat endlessly until `break;` is triggered, so we will need to make a trigger.

```java

while(true) {
    System.out.print("Enter a temperature between -30 and 40: ");
    double value = Double.parseDouble(reader.nextLine());


    if ((value > -31 && value < 41)) {
        Graph.addNumber(value);
        System.out.print("Add another value? (y/n): ");
        String finish = reader.nextLine();
        if (finish.equals("n")) {
            System.out.println("The graph session ended.");
            break;
        }
    } else {
      System.out.println("Value is outside the range");
    }
}

```

The program above begins with asking an user to enter a temperature. It will loop continuously. If the value input is greater than `-31` and less than `41`, then it is added onto the graph. The question will pop out asking if another value is to be entered. `y` will have loop keep rolling. If `n` is entered, then `break;` is triggered. <strong>I made a mistake again... I used an equality operator!</strong> I was stuck on this exercise for awhile, and oh right! Use an `.equals`! Lastly... if value is outside the range, it will be not included into the graph, and will notify the user to try again and this time in the range.  





[MOOC]: https://www.mooc.fi/
[NetBeans]: https://www.netbeans.org
