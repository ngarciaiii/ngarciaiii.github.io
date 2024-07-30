---
layout: post
title:  "Using Derived Tables and Nested SELECT"
date:   2017-06-19 11:48:30
categories: Programming
tags: [SQL]
years: ['2017']
comments: true
---

# Using Subquery and Derived Tables

I had difficult time understanding the `world x` and `world y` concept from the yet completed post "SELECT Quiz". I found this one small hidden hyperlink "SELECT from SELECT" inside another hidden hyperlink "Using nested SELECT" from "SELECT within SELECT", expanding more about derived tables. I am going to cover on that first.

Derived table is when I could use result from one query in another query.

<strong>1)</strong> Subquery with `FROM`

- may use a `SELECT` statement in the `FROM` line
- in this case the derived table `X` has columns `name` and `gdp_per_capita`
- calculated values in the inner `SELECT` can be used in the outer `SELECT`

```sql
SELECT name, ROUND(gdp_per_capita) FROM
  (SELECT name, gdp/population AS gdp_per_capita FROM bbc) X
WHERE gdp_per_capita>20000
```

Happening here:

- <strong>outer query</strong> gather countries that has gdp_per_capita greater than 20000
- <strong>inner query</strong> gather ALL countries with their gdp_per_capita

Noting:

- inner table is given an <strong>alias</strong> `x`
- first column in inner query keeps its `name`
- second column in inner query has an alias `gdp/population AS gdp_per_capita`

| name | ROUND(gdp_per.. |
| Australia | 26900 |
| Austria | 32300 |
| Belgium | 31030 |
| ... |

<br>
<strong>2)</strong> Subquery with `IN`

- find the countries in the same region as Bhutan <br>
- you may use a SELECT statement in the WHERE line - this returns a list of regions

```sql
SELECT name FROM bbc
WHERE region IN (SELECT region FROM bbc WHERE name = 'Bhutan')
```

- no derived table, has a inner query in `WHERE`
- <strong>inner query</strong> identifies the `region` that 'Bhutan' is in
- <strong>outer query</strong> gather all countries in the region yet identified until inner query

| name |
| Afghanistan |
| Bangladesh |
| Bhutan |
| ... |

<br>
<strong>3)</strong> Correlated Subquery

- if a value from the outer query appears in the inner query this is "correlated subquery"
- show the countries where the population is greater than 5 times the average for its region

```sql
SELECT name FROM bbc b1
WHERE population > 5 * (SELECT AVG(population) FROM bbc WHERE region=b1.region)
```

- <strong>outer query</strong> gathers countries `FROM` aliased `bbc b1` table with population greater than 5 times <strong>inner query</strong> result
- <strong>inner query</strong> calculates average population in each region


| name |
| Brazil |
| China |
| India |
| Nigeria |
| Russia |

<br>

# Using Nested SELECT

- result of a SELECT statement may be used as a value in another statement
- statement SELECT continent FROM world WHERE name = 'Brazil' evaluates to 'South America'
- can use this value to obtain a list of all countries in the same continent as 'Brazil'

<strong>1)</strong> Using SELECT in SELECT
List each country in the same continent as 'Brazil'

```sql
SELECT name FROM world
WHERE continent = (SELECT continent FROM world WHERE name = 'Brazil')
```

# Alias

- some versions of SQL insist that you give the subquery an <strong>alias</strong>
- using `AS somename` after the closing bracket

```sql
SELECT name FROM world
WHERE continent = (SELECT continent FROM world WHERE name='Brazil') AS brazil_continent
```

I decided to research a bit more about <strong>alias</strong> and found this juicy information in [wiki][wiki]. It is a feature of SQL that most of relational database management systems (RDBMSs) support.

What <strong>alias</strong> can do:

- reduce the amount of code required for a query
- make simpler to understand
- can be used as an obfuscation technique to protect the real names of database fields
- can alias tables and columns

Alias table is also called a <strong>correlation name</strong>.

# Multiple Results

- subquery may return more than one result
- if more than one result, will fail as testing one value against more than one value
- safer to use `IN` to cope with this possibility

FAIL: `(SELECT continent FROM world WHERE name = 'Brazil' OR name='Mexico')` will return two values ('North America' and 'South America')
{: .redfont}

- Saying "apple" and "orange" at the same time is impossible

BETTER:

```sql
SELECT name, continent FROM world
WHERE continent IN (SELECT continent FROM world WHERE name='Brazil' OR name='Mexico')
```

- <strong>outer query</strong> gather countries and continents
- <strong>inner query</strong> gather continents where 'Brazil' and 'Mexico' are in

<br>
<strong>3)</strong> Subquery on the SELECT line

- if certain that only one value will be returned then can use that query on the SELECT line
- show the population of China as a multiple of the population of the United Kingdom

```sql
SELECT population/(SELECT population FROM world WHERE name = 'United Kingdom')
FROM world WHERE name = 'China'
```

| population/(S.. |
| 21.2987 |


## ALL or ANY

- can use the words ALL or ANY where the right side of the operator might have multiple values

<strong>4)</strong> Show each country that has a population greater than the population of ALL countries in Europe

Note:

- that we mean greater than every single country in Europe
- not the combined population of Europe.

```sql
SELECT name FROM world
WHERE population > ALL (SELECT population FROM world WHERE continent='Europe')
```

| name |
| Bangladesh |
| Brazil |
| China |
| Egypt |
| Ethiopia |
| India |
| Indonesia |
| Japan |
| Mexico |
| Nigeria |
| Pakistan |
| Philippines |
| Russia |
| United States |
| Vietnam |

Now I am heading back to older post [SELECT Quiz][SELECT Quiz] to clarify, since now that I understand a bit more.

[wiki]: https://en.wikipedia.org/wiki/Alias_(SQL)
[SELECT Quiz]: https://ngarciaiii.github.io/sql/2017/06/13/SELECT-Quiz/
