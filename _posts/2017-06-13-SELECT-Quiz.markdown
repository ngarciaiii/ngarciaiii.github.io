---
layout: post
title:  "SELECT Quiz"
date:   2017-06-13 11:48:30
categories: SQL
tags: [SQLzoo]
years: ['2017']
comments: true
---

## UPDATE (06/19/17) Please review [Using Derived Tables and Nested SELECT][Using Derived Tables and Nested SELECT] to understand more about `world x` and `world y` in "Alias" paragraph
{: .redfont}

## New Keywords to learn:

<strong>MAX</strong><br>
Returns the largest value

# world x and world y

Now this is the second half part where <strong>Exercise 4</strong> gets much more complex. Going to do some analysis! The problem states something like this:

Find the largest country (by area) in each continent, show the continent, the name and the area:

```sql
SELECT continent, name, area FROM world x
WHERE area >= ALL (SELECT area FROM world y WHERE y.continent=x.continent
  AND area > 0)
```

| continent | name | area |
| Africa | Algeria | 2381741 |
| Oceania | Australia | 7692024 |
| South America | Brazil | 8515767 |
| North America | Canada | 9984670 |
| Asia | China | 9596961 |
| Caribbean | Cuba | 109884 |
| Europe | Kazakhstan | 2724900 |
| Eurasia |	Russia | 17125242 |

I am wondering if this is considered as ~~multiple tables~~ or still one table, and didn't know there were this many continents too. Two possibly different explanations for this `world x` and `world y`:

- ~~`world x` to search through attributes, and `world y` to search through tuples?~~
- table just duplicated using `x` and `y` to compare each other?

Let's focus on what I understand so far.

- `ALL` means each or every
- `world x` filters for `area` larger than `ALL` area in `world y` continents
- `WHERE` in `world y` filters through and inside continents, and that `y.continent` and `x.continent` are "merged" attributes and tuples?

I assume that other problems are going to be about `world x` and `world y`.

## Exploring more of world x and world y problems!

The next problem states: List each continent and the name of the country that comes first alphabetically.

```sql
SELECT continent, name FROM world x
WHERE name <= ALL(SELECT name FROM world y WHERE y.continent = x.continent)
```

| continent | name |
| Africa | Algeria |
| Asia | Afghanistan |
| Caribbean | Antigua and Barbuda |
| Eurasia | Armenia |
| Europe | Albania |
| North America |	Belize |
| Oceania |	Australia |
| South America |	Argentina |

It appears as if operators `>=` and or `<=` can set attribute in either ascending or descending order. I am not sure if that is the case. This part will <strong>need an UPDATE</strong> later on! I will return to either correct, or confirm it.

## NEED A UPDATE LATER ON! How does Operator `>=` or `<=` cause `name` to sort in order?
{: .redfont}

<br>
Okay! Moving on to the next problem!

The <strong>problem #9</strong> asks for:

- Find the continents where all countries have a population <= 25000000
- Find the names of the countries associated with these continents
- Show name, continent and population

```sql
SELECT name, continent, population FROM world x
WHERE 25000000 > ALL (SELECT population FROM world y WHERE x.continent = y.continent AND y.population > 0)
```

| name | continent | population |
| Antigua and Barbuda |	Caribbean | 86295 |
| Australia | Oceania |	23545500 |
| Bahamas | Caribbean | 351461 |
| Barbados | Caribbean | 285000 |
| Cuba | Caribbean | 11167325 |
| Dominica | Caribbean | 71293 |
| Dominican Republic | Caribbean | 9445281 |
| ... |

Whew! This problem is easier to solve. Draw data on `name`, `continent`, `population` using `world x` table, easy! Filtering for populations with the size of 25000000 or less from every continents. It will return only continents that have `ALL` countries with population less than 25,000,000. I am still having hard time to understand this x table and y table concept. I decide to learn more about database so I can return to explain this better.  

Ugh, another tough problem encountered. The <strong>problem #10</strong> asks for:

- Some countries have populations more than three times that of any of their neighbors (in the same continent)
- Give the countries and continents

```sql
SELECT name, continent FROM world x
WHERE
```

The first step `SELECT` is always easy!

```sql
SELECT name, continent FROM world x
WHERE  population > ALL(SELECT population FROM world y WHERE x.continent = y.continent AND population > 0)
```

Didn't work! I tried to figure out why and I found the answer online. ~~This isn't taught in [SQLZOO][SQLZOO], it can be unfair sometime.~~ More on this was hidden in a hyperlink inside "SELECT within SELECT" on [SQLZOO][SQLZOO]. More information can be found in [Using Derived Tables and Nested SELECT][Using Derived Tables and Nested SELECT]. It is called <strong>aliasing</strong>

The answer looks like this:

```sql
SELECT name, continent FROM world x
WHERE population > ALL(SELECT population*3 FROM world y WHERE x.continent = y.continent AND population > 0 AND y.name != x.name)
```

| name | continent |
| Australia |	Oceania |
| Brazil | South America |
| Russia | Eurasia |

I would have figured the `population*3` part, just not `y.name != x.name`. Makes sense, operator `>` or `<` wouldn't be able to compare if there are two exact same data from "two" tables.

# SELECT QUIZ PART!

## ~~Hope I will understand `world x` and `world y` better through this quiz multiple choices!~~

I would like to note that this Quiz covers a slightly different table. The table is called "bbc", and it uses 'region' instead of 'continent'.  The table looks likes this below:

| name | region | area | population | gdp |
| Afghanistan | South Asia | 652225 | 26000000 |	|
| Albania | Europe | 28728 | 3200000 | 6656000000 |
| Algeria | Middle East | 2400000 | 32900000 | 75012000000 |
| Andorra | Europe | 468 | 64000	| |
| Bangladesh | South Asia | 143998 | 152600000 | 67144000000 |
| United Kingdom | Europe | 242514 | 59600000 | 2022824000000 |
| ... |


<strong>1)</strong> Select the code that shows the name, region and population of the smallest country in each region

```sql
SELECT region, name, population FROM bbc x WHERE population <= ALL (SELECT population FROM bbc y WHERE y.region=x.region AND population>0)
```

Process goes like this:

- <strong>outer query</strong> gathers regions, populations, and countries that are <strong>less or equals</strong> than ALL of <strong>inner query</strong> results
- <strong>inner query</strong> gathers all populations on every regions
- smallest population is gathered from each region

<strong>2)</strong> Select the code that shows the countries belonging to regions with all populations over 50000

```sql
SELECT name,region,population FROM bbc x WHERE 50000 < ALL (SELECT population FROM bbc y WHERE x.region=y.region AND y.population>0)
```

<br>
<strong>3)</strong> Select the code that shows the countries with a less than a third of the population of the countries around it

```sql
SELECT name, region FROM bbc x
WHERE population < ALL (SELECT population/3 FROM bbc y WHERE y.region = x.region
  AND y.name != x.name)
```

- <strong>outer query</strong> gather countries, regions from <strong>correlation name</strong> `bbc x` where population is <strong>less</strong> than ALL <strong>inner query</strong> results
- <strong>inner query</strong> gather population that are reduced to a third from every region and as long as country from bbc x and country from bbc y doesn't compare with each other i.e. (`y.name != x.name`)
- note that it ISN'T <strong>less or equals</strong>    

<br>
<strong>4)</strong>  Select the result that would be obtained from the following code:

```sql
SELECT name FROM bbc
WHERE population > (SELECT population FROM bbc WHERE name='United Kingdom')
   AND region IN (SELECT region FROM bbc WHERE name = 'United Kingdom')
```

| France |
| Germany |
| Russia |
| Turkey |

<br>
<strong>5)</strong>  Select the code that would show the countries with a greater GDP than any country in Africa (some countries may have NULL gdp values)

```sql
SELECT name, gdp FROM bbc x
WHERE gdp > (SELECT MAX(gdp) FROM bbc y WHERE region = 'Africa')
```

- <strong>outer query</strong> gather name and gdp in world that are greater than..
- <strong>inner query</strong> gather the largest gdp from Africa

<br>
<strong>6)</strong> Select the code that shows the countries with population smaller than Russia but bigger than Denmark

```sql
SELECT name FROM bbc
WHERE population < (SELECT population FROM bbc WHERE name='Russia')
   AND population > (SELECT population FROM bbc WHERE name='Denmark')
```

<br>
<strong>7)</strong> Select the result that would be obtained from the following code:

```sql
SELECT name FROM bbc
WHERE population > ALL (SELECT MAX(population) FROM bbc WHERE region = 'Europe')
   AND region = 'South Asia'
```

| Bangladesh |
| India |
| Pakistan |

[SQLZOO]:http://sqlzoo.net/
[Using Derived Tables and Nested SELECT]: https://ngarciaiii.github.io/sql/2017/06/19/Using-Derived-Tables-and-Nested-SELECT/
