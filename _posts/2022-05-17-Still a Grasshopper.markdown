---
layout: post
title: "Still a Grasshopper"
date: 2022-05-17 09:00:00 -0400
categories: Linux
tags: [Basics]
years: ['2022']
comments: true
---

## More of Linux basics

Resuming on [Linux Journey][Linux Journey], and I am in Text-Fu section. It teaches input/output streams. 

```bash
# Standard Out (stdout)
# > is a redirection operator, allow where standard output goes
$ echo Hello World > peanuts.txt

# >> is a redirection operator that prevents overwritten, it appends at end of the file
# >> will create new file if that file doesn't exist
$ echo Hello World >> peanuts.txt

# Standard In
# < is getting inputs from peanut.txt and > is outputting into banana.txt
$ cat < peanuts.txt > banana.txt

```

## stdin, stdout, and stderr

When following thru Text-Fu, I had few questions like why these are called `stdin`, `stdout`, and `stderr`. I assume it is short for "standard input", "standard output", and "error".

```bash
# this outputs a file to a directory, but in this case, a directory that doesn't exist
$ ls /fake/directory > peanuts.txt

# error message would return in the prompt like this below
ls: cannot access /fake/directory: No such file or directory

```

Standard Error does not send message into file, but outputs directly on the screen, so if we want to redirect error message into a file, this is where file descriptors come in. File descriptors for stdin, stdout, and stderr are 0, 1, and 2. 

```bash
# directing error message into file instead of on the screen
$ ls /fake/directory 2> peanuts.txt

# seems like have to be in 100% linux OS, I am on a gnu and this isn't working for me
# supposed to redirect both stdout and stderr to a file
$ ls /fake/directory 2> peanuts.txt 2>&1

# or 
$ ls /fake/directory &> peanuts.txt

# how to dismiss/ignore error messages
$ ls /fake/directory 2> /dev/null
```

In the next subsection, **pipe and tee**,  I have seen and used `|` before many times in the terminal. It's called pipe, looks just like a straight vertical pipeline. Basically piping information into something like `less`. A `tee` is a three ways pipe looking like 'T'. It can write output to two different streams.

```bash
# without pipe and or tee, might be hard to navigate quickly if loooooong list
$ ls -la /etc

# using pipe with less, can navigate quickier, press h in less for help
$ ls -la /etc | less

# write output to two streams, output of lists will be printed into both files. 
$ ls -la /etc | tee peanuts.txt banana.txt

############

# quick useful infomartion about own enivorment
# shows home directory
$ echo $HOME

# shows username
$ echo $USER

# reveals environment variables
$ env

# reveal the path
$ echo $PATH
```

## the cut command, cut it out!

Remember the old ctrl + c, or cmd + c to cut out something. Linux's `cut` is like a swiss army knife version. 


```bash
# cut 5th character out of input in the file
$ cut -c 5 sample.txt

# linux has a delimiter which is new to me, its default delimiter is a TAB
# everything separated by TAB is considered a field
# this cuts field after TAB in the string, keeping the second field
$ cut -f 2 sample.txt

# similar to above, but this time we determine what delimiter is
# this cuts a field before delimiter ";" in the sample txt
$ cut -f 1 -d ";" sample.txt

# more tricks
# cut all characters that are more than 4th, and print the cut characters
$ cut -c 5- sample.txt

# cut all character that are between 5th and 10th and print the cut characters
$ cut -c 5-10 sample.txt

# cut all characters that are less than 6th characters and print the cut characters
$ cut -c -5 sample.txt

############

## paste is like cat, and has delimiter like in cut command. 
# let's create new file with inputs like this one
$ touch sample.txt

$ echo "The" > sample.txt

$ echo "quick" >> sample.txt

$ echo "brown" >> sample.txt

$ echo "fox" >> sample.txt

# remember to use >> so it wouldn't overwrite, and it will append at the end
# sample.txt will have list look exactly like this below
The 

quick

brown

fox

# Time to put paste in use
# paste all together into one liner, -s is short for serial, not sure what that means ¯\_(ツ)_/¯ 
$ paste -s sample.txt
# result looks like 
The     quick   brown   fox

# tab for space looks ugly, lets fix this
# change delimiter from tab to space
$ paste -d ' ' -s sample.txt

# result looks like
The quick brown fox

```

## That's enough for today, Im still a grasshopper. 


[Linux Journey]:https://linuxjourney.com