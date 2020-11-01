# MySQL SELECT

### Introduction to MySQL SELECT statement
The SELECT statement allows you to read data from one or more tables. To write a SELECT statement in MySQL, you follow this syntax:
```
SELECT select_list
FROM table_name;
```
Let’s look at each part of the statement.
- **First,** you start with the **SELECT keyword**. The keyword has a special meaning in MySQL. In this case, SELECT instructs MySQL to retrieve data.
- **Next,** you have space and then a **list of columns or expressions** that you want to show in the result.
- **Then,** you have the **FROM keyword**, space and the name of the table.
- **Finally,** you have a **semicolon ; at the end** of the statement.

The semicolon ; is the ![statement delimiter](https://github.com/Kalpesh14m/MYSQL-Learning/blob/main/Delimiter/README.md). It specifies the end of a statement. If you have two or more statements, you use the semicolon ; to separate them so that MySQL will execute each statement individually.

In the SELECT statement, the SELECT and FROM are keywords and written in capital letters. Basically, ___it is just about formatting___. The uppercase letters make the keywords stand out.

Since ***SQL is not a case-sensitive language***, you can write the keywords in lowercase e.g., select and from, the code will still run.

It is also important to note that the FROM keyword is on a new line. MySQL doesn’t require this. However, placing the FROM keyword on a new line will make the query easier to read and simpler to maintain.

When evaluating the SELECT statement, MySQL evaluates the FROM clause first and then the **SELECT clause**:

![](https://user-images.githubusercontent.com/25608527/97294695-5833e100-1874-11eb-9653-5b3073f0b6d0.png)


### MySQL SELECT statement examples

We will use the table employees in the sample database to demonstrate how to use the SELECT statement:

![](https://user-images.githubusercontent.com/25608527/97294689-5702b400-1874-11eb-84d2-ea913e8a0a58.png)

The table employees has eight columns: employee number, last name, first name, extension, email, office code, reports to, and job title. It also has many rows as shown in the following picture:

![](https://user-images.githubusercontent.com/25608527/97294870-903b2400-1874-11eb-8922-27e899b41c84.png)


#### A) Using the MySQL SELECT statement to retrieve data from a single column example
The following example uses the SELECT statement to select the last names of all employees:
```
SELECT lastName
FROM employees;
```
Here is the partial output:

![](https://user-images.githubusercontent.com/25608527/97295016-cb3d5780-1874-11eb-8798-e1e444e07083.png)

The output of a SELECT statement is called results or a result set as it’s a set of data that results from a query.


#### B) Using the MySQL SELECT statement to query data from multiple columns example
The following example uses the SELECT statement to get the first name, last name, and job title of employees:
```
SELECT 
    lastname, 
    firstname, 
    jobtitle
FROM
    employees;
```    
Even though the employees table has many columns, the SELECT statement just returns data of three columns of all rows in the table as highlighted in the following picture:
    
![ss](https://user-images.githubusercontent.com/25608527/97295169-f4f67e80-1874-11eb-8e97-939a1bda4486.png)
    
The following picture shows the result set:

![ff](https://user-images.githubusercontent.com/25608527/97295144-ef009d80-1874-11eb-870c-ac6838ba6e8b.png)



#### C) Using the MySQL SELECT statement to retrieve data from all columns example
If you want to retrieve data from all the columns of the employees table, you can specify all the column names in the SELECT clause.

Or you just use the **asterisk (*) shorthand** as shown in the following query:
```
SELECT * 
FROM employees;
```
The query returns data from all columns of the the employees table.

***Notes about SELECT star*** The SELECT * is often called “select star” or “select all” since you select all data from a table.

It is a good practice to use the SELECT * for the ad-hoc queries only. If you embed the SELECT statement in the code such as PHP, Java, Python, Node.js, you should explicitly specify the name of columns from which you want to get data because of the following reasons:

The SELECT * returns data from the columns that you may not use. It produces unnecessary I/O disk and network traffic between the MySQL database server and application.

When you explicitly specify the column names, the result set is predictable and easier to manage. However, if you use the SELECT * and someone changes the table by adding more columns, you will end up with a result set that is different from the one that you expected.

Using the SELECT * may expose sensitive information to unauthorized users.


## Use SQL Server Coalesce to Work with NULL Values

**Problem:** Whenever you are using _T-SQL_ to develop queries, you will encounter situations where you have to deal with NULL values. No matter how hard you try, you ***cannot eliminate NULLs***. You can follow best practices when developing your SQL Server database schema, but you still cannot eliminate all NULL values. The simple fact is that you have to allow NULL for some columns and some queries will return NULL values.

The issue with NULL values is that not planning for them being included in your query results will lead to problems. ***How can we deal with detecting NULL values and replacing them with a non-NULL value?***

**Solution:** ***`COALESCE`*** is one of the tools you have in SQL Server to work with NULL values. It may not be the first one you think of, but it can be a very good choice. In this tip I will provide examples of how you can use COALESCE to peacefully coexist with NULL values.

Before we dig in to the details on COALESCE, let's first discuss a few things about NULL in SQL Server and the approach taken in this tip.


### SQL Server Coalesce

When you view COALESCE in SQL Docs, you will find it under `Transact-SQL (T-SQL) Reference / Language elements / Expressions`. Generally speaking, you use the COALESCE expression in the column list of a ***SELECT statement***, although its usage is not limited to the SELECT statement. COALESCE itself takes as arguments a list of 1 to N expressions and returns the value of the first expression that is not NULL.

_COALESCE provides a simple way to **evaluate multiple expressions and determine the first non-null expression** based simply on the order of the expression list_. You can specify your own value to use in the event all of your expression parameters evaluate to NULL. There are situations where ***we require a non-NULL value and COALESCE provides a way for use to assure that we get one.***

### SQL Server versions supported

2005, 2008, 2008R2, 2012, 2104, 2016, 2017, 2019, Azure

### SQL Server Coalesce Usage

The following is from COALESCE in SQL Docs:
Syntax

`COALESCE ( expression [ ,...n ] )`

***Arguments:*** expression is an expression of any type

***The simple example uses COALESCE to return an alternative value for a column that IS NULL***. The following T-SQL query returns the [Tier] for a customer or NONE if the customer [Tier] IS NULL:

**Without COALESCE:**

`select name, age, occupation, abc from employee_table;`

![](https://user-images.githubusercontent.com/25608527/97773814-fd063500-1b78-11eb-98ff-0c4751874430.png)

**With COALESCE:**

`select name, age, occupation, coalesce(abc,"TBD") as myData from employee_table;`

The following are the results:

![](https://user-images.githubusercontent.com/25608527/97773816-00012580-1b79-11eb-9ef8-2f24bf12becb.png)


