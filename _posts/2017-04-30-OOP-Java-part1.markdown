---
layout: post
title:  "OOP Java Part 1"
date:   2017-04-30 4:23:30
categories: Programming
tags: [java]
years: ['2017']
comments: true
---

# UPDATE (06/05/17)
<strong>All classes should be capitalized. I didn't, and started doing that with Week 3.</strong>

# UPDATE (05/23/17)
<strong>Use Netbeans to unlock Mooc.fi Exercises!!!</strong>

# INTRO TO MOOCI.FI

I learn java from [Udemy][Udemy] when I am on my friend's PC and under his account.
Often I am out of town, and I am mostly using my MAC OSX laptop, I learn java from University of Helsinki's [MOOC][MOOC] (Massive Open Online Courses) based in Finland. It uses TMC (Test My Codes) [NetBeans][NetBeans] whereas I use [Eclipse][Eclipse], but I do switch over to NetBeans when exercises have components that are exclusively in Netbeans.

# INSTALL TMC NETBEANS

1) Head over to [downloads][downloads]

- Follow the instructions, and download et cetera et cetera
- Feel free to use either NETBEANS, or ECLIPSE
- On that website, click "START LEARNING"


# OOP JAVA P1 COURSE WEEK 1 BEGINS!

OOP is short for "object oriented programming", Java is basically it. Famous "Hello World!" is already explained in post under category "Udemy". I decided to keep this short and sweet by including exercises that are new to me without needing to cover every exercises. Programming is similar with other different languages such as Python, and JavaScript. Same logic processes, but different syntaxes.

I have been using either `System.out.print();` and `System.out.println();` frequently throughout exercises, so it might be necessary to explain the difference between those. The former prints out and that's it. The latter prints out and adds a new line afterward. The latter with an empty inside `.()` clears the whole line that way exercises and results will be cleaner and more readable. Another way to create new line is using `System.lineSeparator()`. I am going to skip few first exercises and starting with Week 1 Exercise 8 here.  

```java
package usingScanner;

import java.util.Scanner;

public class week1_ex08_12 {
	public static void main(String[] args) {

	}
}
```

A post in Udemy explains top part like `package`, `public class`, and `public static`. I will try to be brief about it. `package` points where file is being saved in, making it easier to direct class file right in. <strong> Class file </strong> is what computer can read, compiles our <strong>java files</strong>. Just let computer worry about class files. That's what Eclipse and or NetBeans do for us. `public` is just saying that other classes can access to that public field or method. Meaning class can manipulate the public method or field if it isn't declared as final.  `static` means can call a method without an object, no need to complicate about it. As more we do java, the better understanding we will come to static and that kind of things. NOTE: `public class ...` has to match with java file's name. For example, java file is saved as `week1_ex08_12`  then it has to be `public class week1_ex08_12`.

All programming languages have <strong>variables</strong>, and it's important to understand how to use it. Each programming languages have same and different types of variables. Java has four types of variables: <i>String, int, double,</i> and <i>booleans</i>.

- <strong>String</strong> uses only alphabetics, and numbers that act as description (not used for mathematical purpose).
- <strong>int</strong>, short for an integer, its value can be either a negative, or a positive number. Always is a whole number and is mostly used for mathematical purpose.   
- <strong>double</strong> is a value that holds decimal number, and always used for mathematical purpose, very useful to any statistics.
- <strong>booleans</strong> hold a value of either <i>true</i>, or <i>false</i>.  

The first differences I noticed between Python, JavaScript and Java is on how to declare a variable. In <strong>Python</strong>, just type out a variable and it will be defined after an operator. In <strong>JavaScript</strong>, a variable is declared after `var`. A variable in <strong>Java</strong> is declared by starting with one of these four types: `String`, `int`, `double`, and or `boolean`. `String` is capitalized, because it is special... it is not just a <strong>primitive</strong> like other three types of variables, it is also a <strong>class</strong>. Anything that is capitalized is probably a class.   

Let's take look at exercise 8 to 12 below. What's new to me is `import java.util.Scanner;`. <strong>Scanner</strong> is used as a parser, for a computer to read the user's input. It cannot read any variables automatically except for a string, it has to be told which kind of variable it is going to read.  

```java
package usingScanner;

import java.util.Scanner;

public class week1_ex08_12 {
	public static void main(String[] args) {
		Scanner reader = new Scanner(System.in);

		System.out.print("Type a number: ");
		int num1 = Integer.parseInt(reader.nextLine());

		System.out.print("Type another number: ");
		int num2 = Integer.parseInt(reader.nextLine());

		int addAns = num1 + num2;

		double divAns = (double) num1 / num2;   

		System.out.println("Sum of the numbers: " + addAns);
		System.out.println("Division: " + divAns + System.lineSeparator());

		System.out.print("Type the radius: ");
		double radius = Double.parseDouble(reader.nextLine());

		double circumference = 2 * Math.PI * radius;

		System.out.println("Circumference of the circle: " + circumference + System.lineSeparator());

		System.out.print("Type your name: ");
		String name1 = reader.nextLine();            

		System.out.print("Type your age: ");
		int age1 = Integer.parseInt(reader.nextLine());

		System.out.print("Type your name: ");
		String name2= reader.nextLine();

		System.out.print("Type your age: ");
		int age2 = Integer.parseInt(reader.nextLine());

		System.out.println(System.lineSeparator() + name1 + " and " + name2 + " are " + (age1 + age2) + " years old in total.");

	}
}
```
First giving Scanner a name `reader`, and declare it to be a Scanner in the system for conventional purpose. `reader.nextLine()` is Scanner waiting to read the user's input right after a "question", and automatically read a string by itself. `.nextLine()` is one of methods inside `Scanner` class. `public` is in a sense "global" methods. `private` is a method created inside a file, where it isn't "global". Back to public or "global" methods, `Integer.parseInt();` says input is going to be an `int`. `Double.parseDouble();` applies for `double`.






[Udemy]: https://www.udemy.com
[MOOC]: https://www.mooc.fi/
[NetBeans]: https://www.netbeans.org
[Eclipse]: http://www.eclipse.org/downloads/packages/
[downloads]: http://mooc.fi/courses/general/programming/how-to-get-started.html
