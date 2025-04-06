# `SQL`
1. [Introduction and Basics](#introduction-and-basics) 
2. [Syntax](#syntax) 
3. [SELECT and FROM](#select-and-from) 
4. [LIMIT](#limit) 
5. [ORDER BY](#order-by) 
6. [WHERE](#where) 
7. [WHERE with Non-Numeric Data](#where-with-non-numeric-data) 
8. [Introduction to Logical Operators](#introduction-to-logical-operators) 
9. [LIKE](#like) 
10. [IN](#in) 
11. [NOT](#not) 
12. [AND and BETWEEN](#and-and-between) 
13. [OR](#or) 
14. [Conclusion](#conclusion)

# `INTRODUCTION and BASICS`

### Introduction :
Before we dive into writing `Structured Query Language (SQL)` queries, let's take a look at what makes SQL and the databases that utilize SQL so popular.

I think it is an important distinction to say that SQL is a language. Hence, the last word of SQL being language. SQL is used all over the place beyond the databases we will utilize in this class. With that being said, SQL is most popular for its interaction with databases. For this class, you can think of a database as a bunch of excel spreadsheets all sitting in one place. Not all databases are a bunch of excel spreadsheets sitting in one place, but it is a reasonable idea for this class.

### Why Do Data Analysts Use SQL?

There are some major advantages to using traditional relational databases, which we interact with using SQL. The five most apparent are:

* SQL is easy to understand.
Traditional databases allow us to access data directly.
* Traditional databases allow us to audit and replicate our data.
* SQL is a great tool for analyzing multiple tables at once.
* SQL allows you to analyze more complex questions than dashboard tools like Google Analytics.
* You will experience these advantages first hand, as we learn to write SQL to interact with data.

### Types of Databases

`SQL Databases`
There are many different types of SQL databases designed for different purposes. In this course we will use [Postgres](https://www.postgresql.org/) which is a popular open-source database with a very complete library of analytical functions.

Some of the most popular databases include:
* MySQL
* SQLite
* Access
* Oracle
* Microsoft SQL Server
* Postgres

You can also write SQL within other programming frameworks like Python, Scala, and HaDoop.

`Small Differences` Each of these SQL databases may have subtle differences in syntax and available functions -- for example, MySQL doesn’t have some of the functions for modifying dates as Postgres. Most of what you see with Postgres will be directly applicable to using SQL in other frameworks and database environments. For the differences that do exist, you should check the documentation. Most SQL environments have great documentation online that you can easily access with a quick Google search.

The article [here](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems) compares three of the most common types of SQL: SQLite, PostgreSQL, and MySQL.


### SQL vs. NoSQL

You may have heard of NoSQL, which stands for `not only SQL`. Databases using NoSQL allow for you to write code that interacts with the data a bit differently than what we will do in this course. These NoSQL environments tend to be particularly popular for web based data, but less popular for data that lives in spreadsheets the way we have been analyzing data up to this point. One of the most popular **NoSQL languages is called `MongoDB`**

### Why Do Businesses Choose SQL?

1. Data integrity is ensured - only the data you want entered is entered, and only certain users are able to enter data into the database.

2. Data can be accessed quickly - SQL allows you to obtain results very quickly from the data stored in a database. Code can be optimized to quickly pull results.

3. Data is easily shared - multiple individuals can access data stored in a database, and the data is the same for all users allowing for consistent results for anyone with access to your database.

<hr>

# `Syntax : `

1. ### Using Upper and Lower Case in SQL

SQL queries can be run successfully whether characters are written in upper- or lower-case. In other words, SQL queries are not case-sensitive , This is because even though SQL is case-insensitive, **it is common and best practice to capitalize all SQL commands, like SELECT and FROM, and keep everything else in your query lower case.**

 2. ### Use White Space in Queries

SQL queries ignore spaces, so you can add as many spaces and blank lines between code as you want, and the queries are the same. 

 3. ### Semicolons

Depending on your SQL environment, your query may need a semicolon at the end to execute. Other environments are more flexible in terms of this being a "requirement." It is considered best practice to put a semicolon at the end of each statement, which also allows you to run multiple queries at once if your environment allows this.

Best practice:
```sql
    SELECT account_id 
    FROM orders;
```
4. ### comments

This is useful if you want to explain what you are doing in your query, or if you want to explain why something is not working.
```sql
-- this is a single line comment
/* multi line comment
another comment */
SELECT account_id 
FROM orders;
```

---

# `SELECT and FROM`

1.  **SELECT**  indicates which column(s) you want to be given the data for.  
    
2.  **FROM**  specifies from which table(s) you want to select the columns. Notice the columns need to exist in this table.

If you want to be provided with the data from all columns in the table, you use "*", like so:

```sql
SELECT * FROM orders
```

Note that using SELECT does not  _create_  a new table with these columns in the database, it just provides the data to you as the results, or output, of this command.

You will use this SQL SELECT statement in every query in this course, but you will be learning a few additional statements and operators that can be used along with them to ask more advanced questions of your data.

<hr>

# `LIMIT`

We have already seen the  **SELECT**  (to choose columns) and  **FROM**  (to choose tables) statements. The  **LIMIT**  statement is useful when you want to see just the first few rows of a table. This can be much faster for loading than if we load the entire dataset.

The  **LIMIT**  command is always the very last part of a query. An example of showing just the first 10 rows of the orders table with all of the columns might look like the following:
```sql 
SELECT * 
FROM orders 
LIMIT 10;
```

We could also change the number of rows by changing the 10 to any other number of rows.

<hr>

# `ORDER BY`
The  `ORDER BY`  command is used to sort the result set in ascending   order.

The  `ORDER BY`  command sorts the result set in ascending order by default. To sort the records in descending order, use the  `DESC`  keyword.

In other words, when you use ORDER BY in a SQL query, your output will be sorted that way, but then the next query you run will encounter the unsorted data again. It's important to keep in mind that this is different than using common spreadsheet software, where sorting the spreadsheet by column actually alters the data in that sheet until you undo or change that sorting. This highlights the meaning and function of a SQL "query."
```sql
SELECT *
FROM orders 
ORDER BY occurred_at 
-- ORDER BY occurred_at DESC; for descending order
LIMIT 10;
```

<hr>

# `WHERE`
Using the **WHERE** statement, we can display _subsets_ of tables based on conditions that must be met. You can also think of the **WHERE** command as _filtering_ the data.
Common symbols used in **WHERE** statements include:
|sign |meaning|
|--|--|
| **>** |greater than|
| **<** | less than |
| **>=** | greater than or equal to |
| **<=** | less than or equal to |
| **=** | equal to |
| **!=** | not equal to |

eg :
```sql
SELECT  *  
FROM orders 
WHERE total_amt_usd <  500  
ORDER BY occurred_at
LIMIT  10;
```

<hr>

# ` WHERE with Non-Numeric Data`

The  **WHERE**  statement can also be used with non-numeric data. We can use the  `=`  and  `!=`  operators here. You need to be sure to use single quotes (just be careful if you have quotes in the original text) with the text data, not double quotes.

Commonly when we are using  **WHERE**  with non-numeric data fields, we use the  **LIKE**,  **NOT**, or  **IN**  operators.

```sql
SELECT name, website, primary_poc 
FROM accounts
WHERE name =  'Exxon Mobil';
```

<hr>

# `Introduction to Logical Operators`

1. `LIKE` This allows you to perform operations similar to using `WHERE and =`, but for cases when **you might not know exactly what you are looking for**.

2. `IN` This allows you to perform operations similar to using `WHERE and =`, but for **more than one condition.**

3. `NOT` This is used with IN and LIKE to select all of the rows `NOT LIKE or NOT IN` a certain condition.

4. `AND` & `BETWEEN` These allow you to `combine operations` where **all combined conditions must be true.**

5. `OR` This allows you to `combine operations` where **at least one of the combined conditions must be true**.

<hr>

# `LIKE`
The LIKE operator is extremely useful for working with text. You will use LIKE within a WHERE clause. The LIKE operator is frequently used with `%`. The % tells us that we might want any number of characters leading up to a particular set of characters or following a certain set of characters, as we saw with the google syntax above. Remember you will need to use single quotes for the text you pass to the LIKE operator, because of this lower and uppercase letters are not the same within the string. Searching for 'T' is not the same as searching for 't'. In other SQL environments (outside the classroom), you can use either single or double quotes.

ex : 
```sql
SELECT * 
FROM accounts 
WHERE domain = 'google';
```
`no results`

```sql
SELECT * 
FROM accounts 
WHERE domain Like '%google%';
```
`all results that have google in the domain`

```sql
SELECT name
FROM accounts
WHERE name LIKE 'C%'; -- starts with C
-- WHERE name LIKE '%C'; -- ends with C
```
`all names that start with C or end with C`

<hr>

# `IN` 

The IN operator is used to select rows that match any of the values specified in the list of values.

ex :
```sql
SELECT * 
FROM accounts 
WHERE name IN ('Exxon Mobil', 'Chevron', 'BP');
```
`all results that have Exxon Mobil, Chevron, or BP in the name`

**it is the same as**
  
```sql
SELECT * 
FROM accounts 
WHERE name = 'Exxon Mobil' OR name = 'Chevron' OR name = 'BP';
```
<hr>

# `NOT`

The **NOT** operator is an extremely useful operator for working with the previous two operators we introduced: IN and LIKE. By specifying **NOT LIKE** or **NOT IN**, we can grab all of the rows that do not meet a particular criteria.

ex :
```sql
SELECT * 
FROM accounts 
WHERE domain NOT Like '%google%';
```
`all results that there domains do not have google `

```sql
SELECT *
FROM web_events
WHERE channel NOT IN ('organic', 'adwords');
```
`all results that there channels do not have organic or adwords `

<hr>

# `AND and BETWEEN`
### `AND :`
The AND operator is used within a WHERE statement to consider more than one logical clause at a time. Each time you link a new statement with an AND, you will need to specify the column you are interested in looking at. You may link as many statements as you would like to consider at the same time. This operator works with all of the operations we have seen so far including arithmetic operators (+, -, *, /) **LIKE** ,**IN** , and **NOT logic can also be linked together using the AND** operator.
> all conditions must be true for a row to be selected.

ex :

1. `Write a query that returns all the orders where the standard_qty is over 1000, the poster_qty is 0, and the gloss_qty is 0.`

```sql
SELECT *
FROM orders
WHERE standard_qty > 1000 AND poster_qty = 0 AND gloss_qty = 0;
```
2. `Using the accounts table, find all the companies whose names do not start with 'C' and end with 's'.`

```sql
SELECT name
FROM accounts
WHERE name NOT LIKE 'C%' AND name LIKE '%s';
```
---
### `BETWEEN :`

Sometimes we can make a cleaner statement using **BETWEEN** than we can using AND. Particularly this is true when we are **using the same column for different parts of our AND statement.** 

`Instead of writing :`
```sql
WHERE column >= 6 AND column <= 10
```
`we can instead write, equivalently:`
```sql
WHERE column BETWEEN 6 AND 10
```
**which is more readable and easier to maintain.**
<hr>

# `OR`

The OR operator is used to combine multiple conditions into a single condition, and is used in conjunction with the WHERE clause. The OR operator is frequently used with LIKE and IN.

> one condition must be true for a row to be selected.

ex :

`Write a query that returns all the orders where the standard_qty is over 1000, the poster_qty is 0, and the gloss_qty is 0.`

```sql
SELECT *
FROM orders
WHERE standard_qty > 1000 OR poster_qty = 0 OR gloss_qty = 0;
```

<hr>

# `CONCLUSION`

In this course, we covered the **basics of PostgreSQL**, including the essential **SELECT** and **FROM** statement **for querying data**, as well as using **LIMIT**, **ORDER BY**, and **WHERE** for **refining results**. We also explored **handling non-numeric data** and working with **logical operators like IN, LIKE, NOT, AND, OR, and BETWEEN** to **build more complex queries**. **This is just the beginning—these foundational skills** will serve as the base for diving deeper into more advanced **PostgreSQL** concepts and database management techniques.
