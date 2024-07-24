---
layout: post
title: "Linux Syntax"
date: 2022-05-12 10:34:00 -0400
categories: PWK
tags: [OSCP]
years: ['2022']
comments: true
---

# Starting with Linux

Following [abatchy.com][abatchy.com]'s "How to prepare for PWK/OSCP, a noob-friendly guide", on the top of a long list is [Linux Journey][Linux Journey]. I am going to read thru the whole thing quickly as I can.

## Learned more about distros

There are several Linux distributions or people call them ***distros***. The most popular options are listed below:

- **Debian** - over 20 years development, extremely stable, and oh yes Kali is Debian-based
- **Red Hat** Enterprise Linux - RHEL in short, most used for enterprise purpose, stricter in distributing
- **Ubuntu** - most popular user-friendly linux, and it is Debian-based too
- **Fedora** - user-friendly Linux, but RHEL-based, basically beta for RHEL before going into RHEL
- **Linux Mint** - essentially Ubuntu lite
- **Gentoo** - hard level linux, own package management Portage
- **Arch** - harder level linux, own package management Pacman, total control of your system
- **openSUSE** - 2nd oldest linux distro, RPM package manager, good for beginner, secured

There are much more Linux distros!

![LinuxDistros](/public/img/linux_distros.webp)


I recommend to use virtual machine, ***VM***, to install Linux distro. Look up youtube on how to install VM and take a pick. Ubuntu is the easiest to start with. I think most of distros are. I haven't tried Arch btw!

## Command Line

Shell is a program that takes commands and sends to OS to perform. "Terminal" and "Console" both are sort of GUI for shell. Linux uses bash (Bourne Again shell). Oh my! Is that why black op elite assassin is given an alisas "Jason Bourne", because he has the ability to execute independently and directly? 

<iframe src="https://giphy.com/embed/orUDTj9Q5TMzTdB892" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

<br>

All in seriousness, it is just author of shell named Stephen Bourne, and bash is superset of earlier shell Bourne. Maybe a Christian pun, "born again"? Anyway there are other type of shells: ksh, zsh, and tsch. Bash seems to be recommended. In prompt, will see either `$` or `#`. `$` is normal user and `#` is superuser or authorized user. Let's list out all commands below! 

```bash
# outputs the current date in day month hour:minute:second AM/PM timezone year format
$ date

# prints out text
$ echo

# to see which directory i am in now, pwd short for 'print working directory'
$ pwd
```

Whoa... I have seen `pwd` and used to think it's a directory to passwords, smh... ah so that what it is!

```bash
# Change Directory
$ cd 

# returns to your home directory
$ cd ~

# takes to the previous directory
$ cd -

###################

# list
$ ls

# list specific directory
$ ls /parent_directory/directory

# list hidden files that starts with .
$ ls -a

# list with detailed long formats
$ ls -l

###################

# create new file, there are more tricks with 'touch' but will show in different post
# 'touch' can replace file by changing timestap
$ touch

# identify what content is in the file
$ file filename

# reads what is in the file, short for concatenate
# can read multiple files
$ cat dogfile birdfile

# viewing large files with several pages, has inner commands
# q to exit, h for help, use arrows to navigate, g to go top of page, G to end of page
$ less filename

###################

# look in history of entered commands
# to search the entered command, ctrl + R
$ history

# to run previous command again
$ !!

# clears up the prompt
$ clear

###################

# copy a file and send it to specific directory
$ cp copiedfile /parent_directory/directory/directory

# copy multiple files and directories using wildcard *
$ cp *.jpg /parent_directory/directory

# copy files and directories within directory recursively (need to practice on this one)
$ cp -r directory/ /parent_directory/directory

# prevents from overwriting filename when copy, i short for interactive
$ cp -i filename /parent_directory/directory

###################

# rename file
$ mv oldfile newfile

# move file to different directory
$ mv filename /parent_directory/directory

# move more than one file to different directory
$ mv filename1 filename2 /parent_directory/directory

# rename directory
$ mv olddirectory newdirectory

# prompt before overwrite file or directory, use i, short for interactive
$ mv -i directory1 directory2

# backup the file by rename the old version (need to practice on this one)
$ mv -b directory 1 directory2

###################

# create new directory or multiple new directories
$ mkdir directory1 directory2

# create new parental directory and subdirectories sametime with -p
$ mkdir -p /parent_directory/directory/subdirectory

###################

# remove a file, warning, its permanent
$ rm filename

# remove forcely
$ rm -f filename

# prompt before delete for good, i for interactive
$ rm -i filename

# to remove entire directory, use -r, short for recursive
$ rm -r directory

# can remove the directory another way
$ rmdir directory

###################

# find specific file in directory
$ find /directory -name filename

# find the type of file or directory, d short for directory
$ find /directory -type d -name foldername

###################

# finding manual page on linux syntax
$ man ls

# brief description on command
$ whatis cat

# create shortcut for commands, but won't save after reboot
# to create permanent alias, save in ~./bashrc
$ alias foobar = 'ls -la'

# remove alias
$ unalias foobar

# closes the shell window
$ exit

```

Okay, there much more to linux syntaxes that I don't know of. I have seen combinations of linux syntaxes that does magic. One person said in the internet about linux basics, that it can be humbling. This post covered most of [Linux Journey][Linux Journey]'s introductory Grasshopper: Getting Started, and Command Line.


[abatchy.com]:https://www.abatchy.com/2017/03/how-to-prepare-for-pwkoscp-noob
[Linux Journey]:https://linuxjourney.com
