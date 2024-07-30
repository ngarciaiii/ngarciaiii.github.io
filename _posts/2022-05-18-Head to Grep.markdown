---
layout: post
title: "Head to Grep"
date: 2022-05-18 09:00:00 -0400
categories: Linux
tags: [Basics]
years: ['2022']
comments: true
---

# Officially going to end the Text-Fu section today!

Ending Text-Fu section in [Linux Journey][Linux Journey]'s Grasshopper part. 

<iframe src="https://giphy.com/embed/VgSjnwSoqiPjRRIJ1F" width="370" height="370" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/dreamworks-mood-lets-do-this-kung-fu-panda-VgSjnwSoqiPjRRIJ1F"></a></p>

## Starting with codeblock

```bash

# head command is when want to see first couple lines of text file
$ head /var/log/syslog

# if want to see 15 lines instead of 2
# -n for number of lines obviously
$ head -n 15 /var/log/syslog

# tail is same concept as head, but at last lines instead
# tail is little different, it is 10 lines by default
$ tail /var/log/syslog
$ tail -n 10 /var/log/syslog

# different feature tail can do
# -f is a "follow" flag, it follows the file as it grow
$ tail -f /var/log/syslog
```

## Getting more complicated, dont be like this panada!

<iframe src="https://giphy.com/embed/EPcvhM28ER9XW" width="480" height="333" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/panda-angry-breaking-EPcvhM28ER9XW"></a></p>


```bash
########################
#
# Linux commands getting strange!
#
# (◔ д◔)_/
# 
# Remember to type --help after each commands for more flags
#
########################

# Not sure what purpose of expand and unexpand is, or why I would be using these, still a newbie
# expand print output with each tab into space
$ expand sample.txt

# unexpand does the opposite to expand, it will change spaces to tabs, -a flag for "all"
$ unexpand -a result.txt

# join command joins multiple files tog and in weird way!
# two files are joined tog by fields. Fields has to be identical, fields like 1, 2, 3. 
file1.txt
1 john
2 jane
3 mary

file2.txt
1 doe
2 doe
3 sue

$ join file1.txt file2.txt
# result:
1 john doe
2 jane doe
3 mary sue

# lets say if two files look like this below: 
file1.txt
john 1
jane 2
mary 3

file2.txt
1 doe
2 doe
3 sue

# fields are in different places now, we want field 2 on file1.txt and field 1 on file2.txt
# flag -1 and -2 are fields 1 and 2, so we are simply assigning field to each file
# non-flag 1 and 2 are simple array order, that's how I read this.
$ join -1 2 -2 1 file1.txt file2.txt
# result:
1 john doe
2 jane doe
3 mary sue

# split is a command that splits up file into different files
# by default, it will split by 1000 lines and file are named by x**, for me first split is xaa
$ split somefile

# sort command is as what it is
$ sort file1.txt

# for reverse sort
$ sort -r file1.txt

# to sort numerically
$ sort -n file1.txt

```

Add `--help` next to each command for more information

<iframe src="https://giphy.com/embed/QxZ0nbcVgMlPlnfZos" width="320" height="320" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/dreamworks-lets-do-this-kung-fu-panda-master-shifu-QxZ0nbcVgMlPlnfZos"></a></p>



```bash

#########################################
#
# This is getting weirder! (;-_-)
#
#########################################

# tr for translate, set characters into another set of characters
# lowcase to caps, have to enter into tr block, and then type hello afterward
# ctrl + c to end or exit
$ tr a-z A-Z 
hello
# result:
HELLO

$ tr -d ello
hello
# result:
h
# apparently it deletes ello from anything


# I like this command, uniq for unique
# this removes duplicates
$ uniq reading.txt


# This counts how many ocurrences of lines/duplicates
$ uniq -c reading.txt

# this is to get the most unqiue value
$ uniq -u reading.txt

# get duplicate values only
$ uniq -d reading.txt

# notes, uniq don't detect duplicates that don't adjacent to each other
# to get uniq detect duplicates that are not in adjacent
$ sort reading.txt | uniq

####################################

# wordcount (wc), total of words in a file
# usually format is numbers of lines, words, characters
$ wc /etc/passwd

# count lines only
$wc -l /etc/passwd

# nl is just weird way of checking number of lines by adding numerals next ot it
$ nl file1.txt

######################################

# This is thing I definitely see all the times! grep
# it search files for characters that match a ceretain pattern, or a string!
$ grep fox sample.txt

# grep can be case insenstive with -i flag
$ grep -i somepattern somefile

# more flexible
$ env | grep -i user

# can use regular expression in pattern
# it returns all .txt in /somedir
$ ls /somedir | grep '.txt$'

# check out egrep and fgrep, use man

```

## The End of Text-Fu section
## Replace "INNER PEACE" with "LINUX KNOWLEDGE"

<iframe src="https://giphy.com/embed/AF7lbthr7cTYI" width="480" height="407" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/quote-red-panda-relevant-AF7lbthr7cTYI"></a></p>





[Linux Journey]:https://linuxjourney.com