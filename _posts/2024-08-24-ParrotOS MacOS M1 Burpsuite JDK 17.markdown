---
layout: post
title: "ParrotOS MacOS M1 Burpsuite JDK 17"
date: 2024-08-24 00:00:00 -0400
categories: Linux
tags: [Fixes]
years: ['2024']
comments: true
---

## Parrot OS unable to open Burpsuite

<iframe width="560" height="315" src="https://www.youtube.com/embed/5IwNUSnOybU?si=xDmDNb_p3sWbzr1u" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<br>
Probably see this when tried to open up a BurpSuite on Parrot OS. It seems that Parrot OS is currently limited to JDK 17. What we will do is downgrade BurpSuite to be compatiable. 

![burp_err](/assets/img//blog/burp_err.png)

## Step 1 Download Burp Community Edition 2021.10.2

Google "Burp Archive Releases, click on the first link [Archive][Archive]

![burp_err](/assets/img//blog/archive.png)

Click on year "2021" and then scroll down to "Professional / Community 2021.10.2" which is highlighted in orange below in the image or click on this link [BurpSuite 2021.10.2][BurpSuite 2021.10.2]
<br>

![burp_err](/assets/img//blog/burp_10_2.png)

**NOTE**: Select "Community" and "JAR" before downloading.
<br>

![burp_err](/assets/img//blog/Community_JAR.png)

## Step 2 Install BurpSuite 2021.10.2
<br>
```bash
user@parrot[~/]:~$ cd Downloads

user@parrot[~/Downloads/]:~$ ls
burpsuite_community_v2021.10.2.jar

user@parrot[~/Downloads/]:~$ sudo mv burpsuite_community_v2021.10.2.jar /usr/share/burpsuite/
```
<br>

Now google "burp JDK 17" and then click on the first link or here [Burp_JDK17][Burp_JDK17]

![Burp_JDK17](/assets/img//blog/Burp_JDK17.png)
<br>

Scroll down and copy the highlighted command from the forum as shown below
![BurpJDK17_forum](/assets/img//blog/BurpJDK17_forum.png)

**NOTE:** be sure to change from `_pro_` to `_community_` in the command

**NOTE:** need add `/usr/share/burpsuite/` after last `UNAMED` as shown below in bash

```bash
java -jar --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.desktop/javax.swing=ALL-UNNAMED /usr/share/burpsuite/burpsuite_community_v2021.10.2.jar
```
<br>


## Ta-Da it worked!

![burp_worked](/assets/img//blog/burp_worked.png)

## Last Step, alias burp command

```bash
user@parrot[~/]:~$ cat ~/.bash_aliases
cat: /home/user/.bash_aliases: No such file or directory

user@parrot[~/]:~$ touch ~/.bash_aliases

user@parrot[~/]:~$ sudo nano ~/.bash_aliases
```

Insert command inside `~/.bash_aliases`

```bash
alias burp='java -jar --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.desktop/javax.swing=ALL-UNNAMED /usr/share/burpsuite/burpsuite_community_v2021.10.2.jar'
```

Almost done!

```bash
user@parrot[~/]:~$ source ~/.bash_aliases

user@parrot[~/]:~$ burp
```
![burp](/assets/img//blog/burp.png)


[Archive]:https://portswigger.net/burp/releases/archive
[BurpSuite 2021.10.2]:https://portswigger.net/burp/releases/professional-community-2021-10-2
[Burp_JDK17]:https://forum.portswigger.net/thread/run-burp-on-openjdk-17-5611cb564e50e

