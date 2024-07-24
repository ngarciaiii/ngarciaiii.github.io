---
layout: post
title:  "SELECT from Nobel"
date:   2017-05-27 10:29:30
categories: SQL
tags: [SQLzoo]
years: ['2017']
comments: true
---

This is the third exercise from [SQLZOO][SQLZOO]. First half of the third exercise is just a review on previous exercises. I don't plan to repeat them. Second half is where it gets harder, and even harder in the next post. This exercise will teach us new SQL tricks, I am going to list some of them below.

## New Keywords to learn

<strong>ORDER BY</strong> <br>
Sort results in order

<strong>ASC | DESC</strong> <br>
When using ORDER BY, can sort in either ascending or descending

# EXERCISE 3 BEGINS!

Database "nobel" we are using looks like this:

| yr | subject | winner |
|-------|-------|-------|
| 1960 | Chemistry | Willard F. Libby |
| 1960 | Literature | Saint-John Perse |
| 1960 | Medicine | Sir Frank Macfarlane Burnet |
| 1960 | Medicine | Peter Madawar |
| ... |

Skipping the first half and starting with the second part. Supposed we want to see all of
the details of these presidential winners below:

- Theodore Roosevelt
- Jimmy character
- Barack Obama

```sql
SELECT *
FROM nobel
WHERE winner IN ('Theodore Roosevelt', 'Jimmy Carter', 'Barack Obama')
```

The asterisk `*` means all. `SELECT *` to gather ALL information/data or on every columns. `WHERE` to filter or search for multiple winners using `IN` and `(...)`.

<strong>Another challenge</strong>, supposed want to see Physics winners for 1980 together with Chemistry winners in 1984? It is probably easy, but good to understand how it works.

```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'Physics' AND yr = '1980' OR subject = 'Chemistry' AND yr = '1984'
```

SQL likes to be long and specific. Filling in can get really long. `OR` is not like `XOR`'s "Either you are with us or against us!". `OR` is in a sense 'AND', but without confusing the computer. If we used `AND` instead of `OR` then it would be overlapping data. Nobody can say "apple" and "orange" at the same time.

<strong>Another great example</strong> of how SQL likes to be long! Show the winners for 1980 excluding Chemistry and Medicine.

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980 AND subject NOT LIKE 'Chemistry' AND subject NOT LIKE 'Medicine'
```

See! Filters for 1980 `AND` subject `NOT LIKE` ... `AND` subject `NOT LIKE` ... <strong>whew!</strong> I wish could be simple like `AND` subject `NOT LIKE` subject1 `OR` subject2. It doesn't work that way.

# Wait a minute, isn't that contradicting?! NEED A UPDATE LATER ON!
{: .redfont}

Why did `AND` works this time when have two different same type of data this time? I guess it's when we use `NOT LIKE`. I will need to return here to clarify when I understand SQL better.

## Different challenges

Find all the details of the prize won by Eugene O'Neill. If you typed `Eugene 0'Neill`. It won't be recognized. This is where SQL gets weird.

```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner = 'Eugene O''Neill'
```

That's right! `"` in the between O and Neill. It is to escape the single quotes. I wonder why not `"Eugene O'Neill"`, but it doesn't work like that.

<strong>This problem</strong> want to find details of winners that has name start with 'Sir'. Show the most recent first the name in order. This is where we get to use `ORDER BY` and `DESC`.

```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC
```

<strong>Last different challenge</strong>, and this one I had hard time with at first. I now understand it. The problem states:

The expression subject IN ('Chemistry','Physics') can be used as a value - it will be 0 or 1.

Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.

That is the challenge, and the clue it had left to us is this below:

```sql
SELECT winner, subject, subject IN ('Physics','Chemistry')
FROM nobel
WHERE yr=1984
ORDER BY subject,winner
```
This is what RESULT will look like.

| winner | subject | subject IN ('.. |
|-------|-------|-------|
| Bruce Merrifield | Chemistry | 1 |
| Richard Stone | Economics | 0 |
| Jaroslav Seifert | Literature | 0 |
| César Milstein | Medicine | 0 |
| Georges J.F. Köhler	| Medicine | 0 |
| Niels K. Jerne | Medicine | 0 |
| Desmond Tutu | Peace | 0 |
| Carlos Rubbia | Physics | 1 |
| Simon van der Meer | Physics | 1 |

Notice how `0` and `1` are not ordered. Subject is ordered alphabetically. This challenge teaches us how to set an order by `0` and `1`. Let's see that works.

```sql
SELECT winner, subject, subject IN ('Physics','Chemistry')
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('Physics','Chemistry'), subject,winner
```

We arranged data in order by `0` and `1` and then subjects and winners alphabetically.

| winner | subject | subject IN ('.. |
|-------|-------|-------|
| Richard Stone | Economics | 0 |
| Jaroslav Seifert | Literature | 0 |
| César Milstein | Medicine | 0 |
| Georges J.F. Köhler	| Medicine | 0 |
| Niels K. Jerne | Medicine | 0 |
| Desmond Tutu | Peace | 0 |
| Bruce Merrifield | Chemistry | 1 |
| Carlos Rubbia | Physics | 1 |
| Simon van der Meer | Physics | 1 |

This challenge doesn't want to see the value in index manner. Taking that `subject IN ('...')` off from `SELECT`.

```sql
SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('Physics','Chemistry'), subject,winner
```

RESULT:

| winner | subject |
|-------|-------|
| Richard Stone | Economics |
| Jaroslav Seifert | Literature |
| César Milstein | Medicine |
| Georges J.F. Köhler	| Medicine |
| Niels K. Jerne | Medicine |
| Desmond Tutu | Peace |
| Bruce Merrifield | Chemistry |
| Carlos Rubbia | Physics |
| Simon van der Meer | Physics |

That's the answer.

## Next post will be EXERCISE 3 still but covering the quiz. New tricks coming up!














[SQLZOO]:http://sqlzoo.net/
