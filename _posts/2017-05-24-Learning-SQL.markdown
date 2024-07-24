---
layout: post
title:  "Learning SQL"
date:   2017-05-24 12:30:30
categories: SQL
tags: [SQLzoo]
years: ['2017']
comments: true
---

I decided to have some exposure on SQL (<i>Structured Query Language</i>). I would like to understand more about SQL and apply my programming skills onto it. This is the first post on SQL, and I am absolutely a beginner. I am sure there will be updates and editions after I dug deep into SQL.

Firstly I want to see if I am able to create a table in this Jekyll Static website. Here goes...

| Priority apples | Second priority | Third priority |
|-------|-------|-------|
| ambrosia | gala | red delicious |
| pink lady | jazz | macintosh |
| honeycrisp | granny smith | fuji |

Wow! It certainly doesn't look like this in Sublime Text 2! Yay, it worked! Going to try a different type of table.

| Priority apples | Second priority | Third priority |
|-------|-------|-------|
| ambrosia | gala | red delicious |
| pink lady | jazz | macintosh |
| honeycrisp | granny smith | fuji |
{:.mbtablestyle}

Hmm... not sure which table I like better. I guess it doesn't matter. SQL will be extracting information from database, and I will make table as an example of what database might look like. I have researched on which is a great tutorial to start with. I decided to start with [SQLZOO][SQLZOO]. Anyway let's start!


# Starting with SELECT basics

## Keywords to learn

<strong>SELECT</strong><br>
Extracting data from a database. Selecting from column1, column2 or field names of the table

<strong>FROM</strong><br>
From what database ...

<strong>WHERE</strong><br>
This clause is used to filter records, it extracts only those that fulfills a specified condition

<strong>IN</strong><br>
Specify multiple values in a WHERE clause, short for multiple OR conditions


<strong>BETWEEN</strong><br>
Selects values in given range, begin and end are included
<br>

## Starting the first exercise / quiz

Let's take a look at what this database called <strong>world</strong> might look like. This <strong>world</strong> database contains information about every countries, continents, areas, and populations from A to Z. I am not going to list all of countries in the table.

| name | continent | area | population |
|-------|-------|-------|-------|
| Afghanistan | Asia | 652230 | 25500100 |
| Albania | Europe | 28748 | 2831741 |
| Algeria | Africa | 2381741 | 37100000 |
| Andorra | Europe | 468 | 78115 |
| Angola | Africa | 1246700 | 20609294 |
| ... |


<strong>1)</strong> The first question is to find <i>countries</i> that has a <i>population</i> between 1,000,000 and 1,250,000. All of the information are in the <strong>world</strong> database. What kind of information do I need to look for in the database?

```sql
SELECT name, population
FROM world
WHERE population BETWEEN 1000000 AND 1250000
```
Easy enough, huh? Name of countries and their population.

<br>
<strong>2)</strong> Second question is pretty much initutive... all the questions are multiple choices. It asks what this SQL code does and what results would look like.

```sql
SELECT name, population
FROM world
WHERE name LIKE "Al%"
```

We know that SELECT is extracting data from columns <i>name</i> and <i>population</i>. FROM world database obviously, and WHERE filters <i>name</i> that is LIKE "Al%". I am guessing that anything that starts with "Al".

Result looks like this:

| name | population |
|-|-|
| Albania | 2831741 |
| Algeria | 37100000 |
{:.mbtablestyle}

<br>
<strong>3)</strong>  Select the code which shows the countries that end in A or L. "Al%" above gave hints, I am guessing using "%a" and "%l", since only the first letter of all countries are capitalized. Notice "%" (placeholder) shows what comes before or after. Also if I used <strong>AND</strong>, it will be confusing because "a" cannot overlap with "l" at end of countries' name. This is the right way to extract the desired data.

```sql
SELECT name
FROM world
WHERE name LIKE "%a" OR name LIKE "%l"
```

<br>
<strong>4)</strong> If want to extract the European countries that have specific number of letters. Take a look below how it should look like.

```sql
SELECT name, length(name)
FROM world
WHERE length(name)=5 and continent = 'Europe'
```

To be honest, I am confused why this uses <strong>and</strong> instead of <strong>AND</strong>. I will research and return to update why.

<br>
<strong>5)</strong> I learned that we could manipulate data from database with mathematic basics. For example:

```sql
SELECT name, area*2
FROM world
WHERE population = 64000
```

Result:

| name | population |
|-|-|
| Andorra | 936 |
{:.mbtablestyle}

What happened is that area is multiplied by 2. Country with the same population is extracted also.

<br>
<strong>7)</strong> Select the code that shows the population density of China, Australia, Nigeria and France.

```sql
SELECT name, population/area
FROM world
WHERE name IN ('China', 'Australia', 'Nigeria', 'France')
```

I think we have covered all usage of keywords, and I skipped the problem #6 because it is easy and involved with greater or lesser operators. Don't worry about it. We will continue on next exercise in different post!

[SQLZOO]:http://sqlzoo.net/
