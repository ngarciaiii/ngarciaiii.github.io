---
layout: post
title:  "SELECT from WORLD"
date:   2017-05-25 00:00:30
categories: SQL
tags: [SQLzoo]
years: ['2017']
comments: true
---

Continuing with tutorial under [SQLZOO][SQLZOO]. The <strong>second exercise</strong> is titled "SELECT from WORLD". Using same <strong>world</strong> database from previous exercise.

| name | continent | area | population | gdp |
|-------|-------|-------|-------|-------|
| Afghanistan | Asia | 652230 | 25500100 | 20343000000 |
| Albania | Europe | 28748 | 2831741 | 12960000000 |
| Algeria | Africa | 2381741 | 37100000 | 188681000000 |
| Andorra | Europe | 468 | 78115 | 3712000000 |
| Angola | Africa | 1246700 | 20609294 | 100990000000 |
| ... |


## New keywords to learn

<strong>XOR</strong><br>
Exclusive OR, it will show data and exclude another data

<strong>ROUND</strong><br>
It rounds the number up. It can round up by tenth, hundredth, and even thousandth. Take a look at an example below.

ROUND(7253.86, 0)    ->  7254 <br>
ROUND(7253.86, 1)    ->  7253.9 <br>
ROUND(7253.86,-3)    ->  7000 <br>
<br>

# EXERCISE 2 BEGINS!

## One or the other (but not both)
I learned a new trick, using <strong>XOR</strong>. It is short for Exclusive OR, which accepts only one of either if two desires are given. Take a look at an example below:

- Australia has a big area but a small population, it should be <strong>included</strong>.
- Indonesia has a big population but a small area, it should be <strong>included</strong>.
- China has a big population and big area, it should be <strong>excluded</strong>.
- United Kingdom has a small population and a small area, it should be <strong>excluded</strong>.

Their definition of big `population` is `>250000000` and big `area` as `>3000000`.

```sql
/* one or the other */
-- just not two BIGS together

SELECT name, population, and area
FROM world
WHERE population > 250000000 XOR area >3000000
```

RESULT:

| name | population | area |
|-------|-------|-------|
| Australia | 23545500 | 7692024 |
| Brazil | 202794000 | 8515767 |
| Canada | 35427524 | 9984670 |
| Indonesia | 252164800 | 1904569 |
| Russia | 146000000 | 17125242 |

What's happening here is that `XOR` select only one that has either big population, OR big area. BIG population AND BIG area data are excluded.

## Rounding

This problem wants me to:
- show the `name`, `population` in millions, and `gdp` in billions
- in `continent` 'South America'
- use `ROUND` to show values in two demical places

So here goes!

```sql
SELECT name,
   ROUND(population/1000000, 2),
   ROUND(gdp/1000000000, 2)
FROM world
WHERE continent = 'South America'
```

| name | ROUND(populat.. | ROUND(gdp/100.. |
|-------|-------|-------|
| Argentina | 42.67 | 477.03 |
| Bolivia |	10.03 | 27.04 |
| Brazil | 202.79 | 2254.11 |
| Chile | 17.77 | 268.31 |
| Colombia | 47.66 | 369.81 |
| Ecuador | 15.77 | 87.50 |
| Guyana | 0.78 | 2.85 |
| Paraguay | 6.78 |	25.94 |

Isn't that cool?


## Name and capital have the same length

There is another way to use `LENGTH`, which is different from other programming languages.

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital)
```

What it does is searching for data of countries that has the same number of letters as their own capital.

## Matching name and capital

- First letter of name and capital has to match
- name and capital cannot be the same word

In this problem, I learned the function of `LEFT`. It means left side and it can be used to isolate the first letter. I also learned the NOT EQUAL operator `<>`.

```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name <> capital
```

The result will list all countries and capitals that share the same first alphabetic letter and exclude these that have fully the exact same spellings.

## All the vowels

- if name has more than one word, or a space in the between, reject or ignore.
- find the country that has all the vowels and no space in its name  

This is the hardest problem so far. I wasn't sure how to do it right. Now I understand how to do it properly. I thought could use commas. Nope, just has to do it in long way.

```sql
SELECT name
    FROM world
WHERE name LIKE '%a%'
    AND name LIKE  '%e%'
    AND name LIKE  '%i%'
    AND name LIKE '%o%'
    AND name LIKE '%u%'
    AND name NOT LIKE '% %'
```

Notice `%..%`, it means placeholder is anywhere. So I searched for vowels anywhere in the word. Also could use `NOT LIKE` to exclude the character. Only one country that has all the vowels in it is Mozambique.

## Ending this exercise

Quiz should be easy! I am not going to cover them. I decided to try this [Find the duplicate][duplicate] game. It begs the question, why and what it has to do with the SQL? I am guessing, to improve our eagle eyes against overwhelming data. It's fun and challenging! My first score was 11, but didn't realize that not all has to match, just <strong>keys</strong>. My second attempt, its 15! On my third try, finished the game.  


[SQLZOO]:http://sqlzoo.net/
[duplicate]:http://sqlzoo.net/brain/bt.htm#
