---
layout: post
title:  "SELECT within SELECT"
date:   2017-06-13 01:29:30
categories: SQL
tags: [SQLzoo]
years: ['2017']
comments: true
---

SELECT within SELECT exercise in [SQLZOO][SQLZOO] teaches how to perform complex queries with one table. I am still new to SQL and yet have to learn how to work with two different tables or more.

## New Keywords to learn

<strong>CONCAT</strong> <br>
Its function is used to concatenate two strings to form a single string

<strong>ALL</strong> <br>
This operator returns true if all of the subquery values meet the condition

# Exercise 4

## "world" table

| name | continent | area |	population | gdp |
| Afghanistan |	Asia | 652230 | 25500100 | 20343000000 |
| Albania |	Europe | 28748 | 2831741 | 12960000000 |
| Algeria |	Africa | 2381741 | 37100000 | 188681000000 |
| Andorra |	Europe | 468 | 78115 | 3712000000 |
| Angola | Africa | 1246700 | 20609294 | 100990000000 |
| ... |
{:.mbtablestyle}
<br>


The most basic form of using `SELECT` within `SELECT`  looks something like this:

```sql
SELECT name FROM world
WHERE population > (SELECT population FROM world WHERE name = 'Russia')
```

Showing list of `name` from table `world` and filtering for `population` that is larger than `population` from table `world` with `name` of `'Russia'`. Extracting two different information from same column `population` to compare.

We could gather three or more different information from same column if needed. For example, if somebody want to find which countries that have larger population than Canada but less than Poland. Would like to see result showing names and populations to confirm.  

```sql
SELECT name, population FROM world
WHERE population >  (SELECT population FROM world WHERE name = 'Canada')
  AND population < (SELECT population FROM world WHERE name = 'Poland')
```

RESULT:

| name | population |
| Iraq | 36004552 |
| Sudan |	37289406 |

<br>

# Using CONCAT

Germany (population 80 million) has the largest population of the countries in Europe. Austria (population 8.5 million) has 11% of the population of Germany.

- Show the name and the population of each country in Europe
- Show the population as a percentage of the population of Germany

I got stuck with this problem for awhile because of a silly mistake and few other reasons which I will explain.

<strong>A silly mistake</strong>

```sql
SELECT name,
  CONCAT(ROUND(population/(SELECT population FROM world WHERE name='Germany'), 0), %)
FROM world
WHERE population IN (SELECT population FROM world WHERE continent='Europe')
```

Didn't produce any result, I got stuck on that for awhile, A LONG AWHILE. Silly mistake, I thought `%` was actually an operator for SQL. It's just a string or a percentage symbol at least, and I was missing ''. Now let's see if the second change is successful...

<strong>2nd change in coding</strong>

```sql
SELECT name,
  CONCAT(ROUND(population/(SELECT population FROM world WHERE name='Germany'), 0), '%')
FROM world
WHERE population IN (SELECT population FROM world WHERE continent='Europe')
```

The result arrived with a long list of nations having <strong>0%</strong> while few of them having <strong>1%</strong>. Something must be off. I suspected that it must have something to do with `ROUND` and decimal position `0`. I decided to change from `0` to `2`. Let's see what happens.  

```sql
SELECT name,
  CONCAT(ROUND(population/(SELECT population FROM world WHERE name='Germany'), 2), '%')
FROM world
WHERE population IN (SELECT population FROM world WHERE continent='Europe')
```

RESULT:

| name | CONCAT(ROUND(.. |
| Albania |	0.03% |
| Andorra |	0.00% |
| Austria |	0.11% |
| Belarus |	0.12% |
| Belgium |	0.14% |


Ah-ha! I am getting there! Still little bit off. To be honest, I cheated a little bit. In [SQLZOO][SQLZOO], although it doesn't give off a solution, it gives what an answer should look like. Anybody could deduce that it takes 100 * 0.03% to = 3% as it should be.  

<strong> Another change </strong>

```sql
SELECT name,
  CONCAT(ROUND((population*100)/(SELECT population FROM world WHERE name='Germany'), 2), '%')
FROM world
WHERE population IN (SELECT population FROM world WHERE continent='Europe')
```  

RESULT:

| name | CONCAT(ROUND(.. |
| Albania |	3.50% |
| Andorra | 0.09% |
| Austria |	10.54% |
| Belarus |	11.73% |
| Belgium	| 13.87% |


Still incorrect, because decimal is present. Time to change `2` back to `0`

<strong>Last change</strong>

```sql
SELECT name,
  CONCAT(ROUND((population*100)/(SELECT population FROM world WHERE name='Germany'), 0), '%')
FROM world
WHERE population IN (SELECT population FROM world WHERE continent='Europe')
```  

RESULT:

| name | CONCAT(ROUND(.. |
| Albania | 3% |
| Andorra | 0% |
| Austria | 11% |
| Belarus | 12% |
| Belgium | 14% |

<br>

# Using ALL

`ALL` is a fast way of checking the list in the table. Supposed we want to know which countries that have greater GDP than every countries in Europe. Can't be that many..

```sql
SELECT name FROM world
WHERE gdp > ALL ( SELECT gdp FROM world WHERE continent = 'Europe' AND gdp > 0)
```

`gdp > 0` is necessary, because some gdp might have blank or `null` values.
Only three countries that have gdp greater than every countries in Europe are USA, China, and Japan.

## I am going to stop this EXERCISE in half, and post the second half next 'SELECT Quiz'.

## It requires more analyzing and explaining. It involves using `world x` and `world y`. I will also cover the QUIZ in the same post.

## UPDATE (06/19/17) Go to [Using Derived Tables and Nested SELECT][Using Derived Tables and Nested SELECT] post before "SELECT Quiz"
{: .redfont}

[SQLZOO]:http://sqlzoo.net/
[Using Derived Tables and Nested SELECT]: https://ngarciaiii.github.io/sql/2017/06/13/SELECT-within-SELECT/
