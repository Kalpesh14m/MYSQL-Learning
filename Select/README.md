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

The semicolon ; is the ![statement delimiter](). It specifies the end of a statement. If you have two or more statements, you use the semicolon ; to separate them so that MySQL will execute each statement individually.

In the SELECT statement, the SELECT and FROM are keywords and written in capital letters. Basically, ___it is just about formatting___. The uppercase letters make the keywords stand out.

Since ***SQL is not a case-sensitive language***, you can write the keywords in lowercase e.g., select and from, the code will still run.

It is also important to note that the FROM keyword is on a new line. MySQL doesn’t require this. However, placing the FROM keyword on a new line will make the query easier to read and simpler to maintain.

When evaluating the SELECT statement, MySQL evaluates the FROM clause first and then the **SELECT clause**:

![](https://user-images.githubusercontent.com/25608527/97294695-5833e100-1874-11eb-9653-5b3073f0b6d0.png)

#### MySQL SELECT statement examples

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
