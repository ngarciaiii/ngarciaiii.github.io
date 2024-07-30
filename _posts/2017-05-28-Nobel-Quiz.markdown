---
layout: post
title:  "Nobel Quiz"
date:   2017-05-27 10:29:30
categories: Programming
tags: [SQL]
years: ['2017']
comments: true
---

This post covers [SQLZOO][SQLZOO]'s <strong>Exercise #3 Quiz</strong>. In previous post "SELECT from Nobel", few new tricks like how to arrange data in order was discussed. It is also pointed out that SQL like things to be written out in a long way. We will notice that here.

## New Keywords to learn

<strong>DISTINCT</strong> <br>
Return "different" values, or would ignore duplicate values

<strong>NOT IN</strong> <br>
Select things that are NOT IN literally.


## "nobel" database

| yr | subject | winner |
|-------|-------|-------|
| 1960 | Chemistry | Willard F. Libby |
| 1960 | Literature | Saint-John Perse |
| 1960 | Medicine | Sir Frank Macfarlane Burnet |
| 1960 | Medicine | Peter Madawar |
| ... |

<br>
<br>
<strong>1)</strong> Write the code that shows the name of winner's names beginning with C and ending in n.

```sql
SELECT winner FROM nobel
WHERE winner LIKE 'C%' AND winner LIKE '%n'
```

Told ya! SQL likes to be long. Wait... it's going to be even longer.
<br>

<br>
<strong>3)</strong> Write the code that shows the amount of years where no Medicine awards were given. This is new to me. I wouldn't have guessed it. The quiz is multiple choices. It is written out like this:

```sql
SELECT COUNT(DISTINCT yr) FROM nobel
WHERE yr NOT IN (SELECT DISTINCT yr FROM nobel WHERE subject = 'Medicine')
```

`DISTINCT` is "different", removing the duplicates. So what's happening here:

- `SELECT COUNT(DISTINCT yr)` counts the years, excluding duplicates
- `WHERE yr NOT IN (...)` filters for the years that are not in... ()
- `(SELECT DISTINCT yr FROM nobel WHERE subject = 'Medicine')` find year (excluding duplicates) where 'Medicine' were won

Let's try again in English: Count the years that are not duplicates and that doesn't have a 'Medicine' award in the same year. Wow it takes some brainpower. I am up for this challenge.
<br>

<br>
<strong>5)</strong> Write the code which would show the year when neither a Physics or Chemistry award was given.

```sql
SELECT yr FROM nobel
WHERE yr NOT IN (SELECT yr FROM nobel WHERE subject IN ('Physics', 'Chemistry'))
```
Admittedly, I made mistakes few times, and struggled with these. I am not used to this new concept <strong>YET</strong>, but practices make perfect.
<br>


<br>
<strong>6)</strong> Write the code which shows the years when a Medicine award was given but no Peace or Literature award was.

```sql
SELECT yr FROM nobel
WHERE subject = 'Medicine'
  AND yr NOT IN (SELECT yr FROM nobel WHERE subject = 'Peace')
  AND yr NOT IN (SELECT yr FROM nobel WHERE subject = 'Literature'))
```
This one is definitely long one. I got this one wrong too. I think I am understanding it more now.
<br>


<br>
<strong>7)</strong> What will the result that would be obtained from the following code:

```sql
SELECT subject, COUNT(subject) FROM nobel
WHERE yr ='1960'
GROUP BY subject
```

|-------|-------|
| Chemistry | 1 |
| Literature | 1 |
| Medicine | 2 |
| Peace | 1 |
| Physics | 1 |
{:.mbtablestyle}

I sure botched this quiz, but after doing blog on this, my confidence increased.





[SQLZOO]:http://sqlzoo.net/
