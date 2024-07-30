---
layout: post
title:  "Intro to Java"
date:   2017-04-19 3:02:30 -0400
categories: Programming
tags: [java]
commets: true
years: ['2017']
---

I am learning how to do Java via [Udemy][Udemy], so let's get started. BTW, I use Mac OSX.

# SET UP

1) Download the Java SE JDK latest version at [Oracle][Oracle].

  - Accept License Agreement
  - Double click to install
  - Open a terminal shell and type java -version to see if it's in.
  - It should be in a path that looks like this /Library/Java/JavaVirtualMachines/
  - open .bash_profile in terminal shell by `open ~ .bash_profile`
  - add `export JAVA_HOME='/usr/libexec/java_home'` to .bash_profile, so JAVA_HOME is always set.   (Note that `' ... '` between /usr/libexc... are actually back-ticks)

2) Download the Eclipse IDE for Java Developers from [Eclipse][Eclipse].

  - Click 'Eclipse IDE for Java Developers' to install
  - Open finder, and double click on Eclipse application to fully install.
  - Move it into Applications from Downloads.

# All SET and now the first exercise!

Java is an object oriented language (OOP). ~~Objects in Java are called "classes"~~. Objects are instances of Classes. Classes are in other word templates or files.

The whole process looks like filename.java --> javac (compiler) --> .class file (byte codes) --> Outputs (Java Virtual Machines i.e. Window, Mac, and Linux). I think by now, everybody knows the first exercise is always "Hello World!", yep we are doing that.

Create a file named `Hello.java` in a new folder `exercises`, and fill these codes inside then save it.


```java

package exercises;

public class Hello {
  public static void main(String[] args) {
    System.out.print("Hello, ");           
    if (args.length == 0) {
      System.out.println("World!");
    } else {
      System.out.println(args[0] + "!");
    }
  }
}
```

`package` is pinpointing to a folder that holds the file, declares path <br />
`public` lets know that anyone can access it <br />
`static` means `main` is not needed to run it <br />
`void` declares that this method doesn't return a value <br />
`main` is just a name of the method <br />
`System` is a pre-defined class that Java provides us, has useful methods and variables <br />
`out` a static variable for "output" within System <br />
`println` is a method short for "print a line" <br />

No worries, I don't understand most of these yet.

The whole set of codes inside brackets after `main` is called a method. The parameter has two arguments `String[]` and `args`. I am not sure why there're square brackets by `String`. It's associated with array. Give me time, I am new to Java.

`System.out.println` obviously prints "Hello " when it is being run, and there are conditional statements. `if` that says if args.length is 0 or in another word, empty, then it is "World!", printing out "Hello World!" in complete. `else` operates if args isn't empty, and that args is printed out instead of "World!" and then is added an exclamation to it.

Open terminal shell and follow step by step below:

- `cd` to the `exercises` directory
- `ls` to see what files are stored in the `exercises` directory, probably just a `Hello.java` file
- `javac Hello.java` compiling the file to .class file
- Type `ls` again, and should see `Hello.class`, meaning it's working
- `java Hello` and should see "Hello World!" printed out
- `java Hello Bob` and then should see "Hello Bob!" printed out






[Udemy]: https://www.udemy.com
[Oracle]: https://www.oracle.com/technetwork/java/javase/downloads/index.html
[Eclipse]: http://www.eclipse.org/downloads/packages/
