---
layout: post
title:  "Introduction and Relational Databases"
date:   2017-06-15 08:09:30
categories: databases
tags: [Stanford]
years: ['2017']
comments: true
---

I was learning SQL through [SQLZOO][SQLZOO], and at first, it looks easy. The deeper I got into it, and I realized that it can become all gibberish. I figured it might have to do with me not understanding the database entirely. I decided to learn database in order to be able use SQL proficiently. I will be using this blog to act as a note on what I learned about databases. I will be learning about database via [Stanford University][Stanford University] online course.

## Keywords to learn

<strong>Database Management Systems (DBMS)</strong><br>
It provides a means of handling large amount of data primarily

<strong>concurrency control</strong><br>
Used to address conflicts with the simultaneous accessing or altering of data that can occur with a multi-user system

<strong>physical data independence</strong><br>
Data stored in database and directly unaffected or unadulterated by external users/programs, data remains the same

<strong>attributes</strong><br>
Another word for columns in database, each has a type or a domain like int, float, jpeg file

<strong>tuples</strong><br>
Another word for rows in database, hold values

# Introduction

## Why database?

- can hold number of terabytes data daily!   
- outlives any programs that execute on that data
- preserves data, keeping them consistent regardless of what happens, such as a malfunction with: hardware, software, power, and users
- allows concurrency control where multi-users can access to and use data without overwriting
- designed to work easily with large amounts of data

<strong>Physical data independence</strong> is what makes database useful. Users and programs can do whatever with the data, but data in the database will remains the same, unmoved. Databases are usually queried by <strong>query languages</strong> that are relatively compact to describe the algorithm to get the data out. Query language is very <strong>declarative</strong>.

Database systems are often used in conjunction with <strong>middle-ware</strong>. Middle-ware might be application servers, web servers which help application to interact with database system.

## There are <strong>four key concepts</strong> to start with:

<strong>data model</strong><br>
the description of how the data is structured, often in relational dot. Data would be in a <strong>set of records</strong>. Currently, popular format is <strong>XML document</strong> to store data. Another is <strong>graph data model</strong>.

<strong>schema versus data</strong><br>
Schema are types while data are variables. Database is sometime adhered to schema, which tells the structure of the database, to find where specific data are. Usually, schema is set up at the beginning.   

<strong>data definition language (DDL)</strong><br>
DDL is used to set up schema or structure for a particular database.

<strong>data manipulation or query language (DML)</strong><br>
DML is used to querying or modifying the data.

## <strong>Four key people</strong> involved with database:

<strong>DBMS implementer</strong><br>
Sets up system or database.

<strong>Database designer</strong><br>
Establish schema for databases.

<strong>Database application developers</strong><br>
Builds an application that runs on the database, interfacing between eventual user and the data itself.

<strong>Database administrator</strong><br>
Loads data and keeps it running smoothly.

Database systems have a number of tuning parameters associated. Can make a significant difference in the all important performances.

# The Relational Model

- Database is a set of <strong>relations</strong> or <strong>tables</strong>
- Each relation has a set of named <strong>attributes</strong> or <strong>columns</strong>
- Each <strong>tuple</strong> or <strong>row</strong> has a value for each attribute

Let's take a look at the relation <strong>Student</strong> below:
![student relation](/public/img/databases/Slide1.png){: .center-image }

Each attribute has a <strong>type</strong> like int, or float, and or jpeg file. Type is sometime referred as a <strong>domain</strong>.

We can see <strong>schema</strong> in relation <strong>Student</strong>, mostly starting with attributes. Attributes are filled with <strong>instances</strong>. Instances are actual content at given point in time, and these do change over the time.

Schema decide to have data of ID, Name, GPA, and Photo. These are instances help identifying a "student" in table <strong>Student</strong>. Attributes is encouraged to be a detectable unique character or <strong>key</strong>. Key is attribute whose value is unique in each tuple.

Look at different relation <strong>College</strong>:
![college relation](/public/img/databases/Slide2.png){: .center-image height="300px" width="375px"}

There are probably <strong>SEVERAL colleges with SAME NAME "Washington"</strong>, so it <strong>CAN'T</strong> be really a <strong>key</strong> BUT if state is added next to it. <strong>Two combined values of attributes together CAN</strong>  become a <strong>key</strong>. Key is effective when used as a target for query.

## Creating table in SQL

```sql
create Table Student(ID, Name, GPA, Photo)
```

Another example:

```sql
create Table College(name string, state char(2), enrollment integer)
```


# Querying Relational Databases

The basic steps in creating and using relational database goes:

- design the schema
- create the schema using DDL (starting with attributes)
- load up the database with initial data (usually from external source)

People have tendency of drawing database as a barrel or a massive disk.
<br>

![database](/public/img/databases/Slide3.png){: .center-image height="370px" width="auto"}

After that, the next step would be:

- query and modify the data
- might need to update or insert new data later on

A person who wants to use the database would ask queries and database will provide answers.

Queries would be such:

- all students with GPA > 3.7 applying to Stanford and MIT only
- all engineering departments in CA with < 500 applicants
- college with highest average accept rate over last 5 years

When a query 1 would goes over the relations and "create a new relation", it is called <strong>closed</strong>. If there's a query 2 coming up and covers the "new relation", and existing relations then it is <strong>compositionality</strong>.

![closed, compositional](/public/img/databases/Slide4.png)

## Query languages

<strong>Relational Algebra</strong><br>
It is a formal language, a very theoretically well-grounded.

<strong>SQL</strong><br>
An actual language, implemented language. It does have a foundation relational algebra. Semantics are defined.




[SQLZOO]:http://sqlzoo.net/
[Stanford University]:https://lagunita.stanford.edu/courses/DB/2014/SelfPaced/about
