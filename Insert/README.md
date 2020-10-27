# MySQL Insert

## MySQL INSERT statement
The INSERT statement allows you to insert one or more rows into a table. The following illustrates the syntax of the INSERT statement:
```
INSERT INTO table(c1,c2,...)
VALUES (v1,v2,...);
```
In this syntax,

**First,** specify the table name and a list of comma-separated columns inside parentheses after the INSERT INTO clause.

**Then,** put a comma-separated list of values of the corresponding columns inside the parentheses following the VALUES keyword.

The number of columns and values must be the same. In addition, the positions of columns must be corresponding with the positions of their values.

To insert multiple rows into a table using a single INSERT statement, you use the following syntax:
```
INSERT INTO table(c1,c2,...)
VALUES 
   (v11,v12,...),
   (v21,v22,...),
    ...
   (vnn,vn2,...);
```
In this syntax, rows are separated by commas in the VALUES clause.

**MySQL INSERT examples**

Let’s create a new table named tasks for practicing the INSERT statement.
```
CREATE TABLE IF NOT EXISTS tasks (
    task_id INT AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    start_date DATE,
    due_date DATE,
    priority TINYINT NOT NULL DEFAULT 3,
    description TEXT,
    PRIMARY KEY (task_id)
);
```

---

### 1) MySQL INSERT – simple INSERT example
The following statement inserts a new row into the tasks table:
```
INSERT INTO tasks(title,priority)
VALUES('Learn MySQL INSERT Statement',1);
```
MySQL returns the following message:

`1 row(s) affected`

It means that one row has been inserted into the tasks table successfully.

This query returns data from the tasks table:

`SELECT * FROM tasks;`

Here is the output:

![](https://user-images.githubusercontent.com/25608527/97344812-458acd80-18af-11eb-8948-f446b0196da2.png)

In this example, we specified the values for only title and priority columns. For other columns, MySQL uses the default values.

The task_id column is an **AUTO_INCREMENT column**. It means that ***MySQL generates a sequential integer whenever a row is inserted into the table.***

The start_date, due_date, and description columns use **NULL as the default value**, therefore, MySQL uses NULL to insert into these columns if you don’t specify their values in the INSERT statement.

---

### 2) MySQL INSERT – Inserting rows using default value example
If you want to insert a default value into a column, you have two ways:

- Ignore both the column name and value in the INSERT statement.
- Specify the column name in the INSERT INTO clause and use the DEFAULT keyword in the VALUES clause.
    
The following example demonstrates the second way:
```
INSERT INTO tasks(title,priority)
VALUES('Understanding DEFAULT keyword in INSERT statement',DEFAULT);
```
In this example, we specified the priority column and the  **DEFAULT keyword.**

Because the default value for the column priority is 3 as declared in the table definition:

`priority TINYINT NOT NULL DEFAULT 3`

MySQL uses the number 3 to insert into the priority column.

The following statement returns the contents of the tasks table after the insert:

`SELECT * FROM tasks;`

Here is the output:

![](https://user-images.githubusercontent.com/25608527/97344868-576c7080-18af-11eb-9fc6-0a1a38fb5cfe.png)

---

### 3) MySQL INSERT – Inserting dates into the table example
To insert a literal date value into a column, you use the following format:

`'YYYY-MM-DD'`

In this format:

- `YYYY` represents a four-digit year e.g., 2018.
- `MM` represents a two-digit month e.g., 01, 02, and 12.
- `DD` represents a two-digit day e.g., 01, 02, 30.

The following statement inserts a new row to the tasks table with the start and due date values:
```
INSERT INTO tasks(title, start_date, due_date)
VALUES('Insert date into table','2018-01-09','2018-09-15');
```
The following picture shows the contents of the tasks table after the insert:

![](https://user-images.githubusercontent.com/25608527/97344950-7a972000-18af-11eb-8449-c3bf8e6756d8.png)

It is possible to use expressions in the VALUES clause. For example, the following statement adds a new task using the current date for start date and due date columns:
```
INSERT INTO tasks(title,start_date,due_date)
VALUES('Use current date for the task',CURRENT_DATE(),CURRENT_DATE())
```
In this example, we used the **CURRENT_DATE() function** as the values for the start_date and due_date columns. Note that the CURRENT_DATE() function is a date function that returns the current system date.

Here are the contents of the tasks table after insert:

![](https://user-images.githubusercontent.com/25608527/97344957-7c60e380-18af-11eb-929b-03c66dc567bf.png)

---

### 4) MySQL INSERT – Inserting multiple rows example
The following statement inserts three rows into the tasks table:


To insert multiple rows into a table, you use the following form of the INSERT statement:
```
INSERT INTO table_name (column_list)
VALUES
	(value_list_1),
	(value_list_2),
	...
	(value_list_n);
```
In this syntax:
- **First,** specify the name of table that you want to insert after the INSERT INTO keywords.
- **Second,** specify a comma-separated column list inside parentheses after the table name.
- **Third,** specify a comma-separated list of row data in the VALUES clause. Each element of the list represents a row. The number of values in each element must be the same as the number of columns in the column_list.
```
INSERT INTO tasks(title, priority)
VALUES
	('My first task', 1),
	('It is the second task',2),
	('This is the third task of the week',3);
```
In this example, each row data is specified as a list of values in the VALUES clause.

MySQL returns the following message:

`3 row(s) affected Records: 3  Duplicates: 0  Warnings: 0`

It means that the three rows have been inserted successfully with no duplicates or warnings.

`SELECT * FROM tasks;`

The table tasks has the following data:

![](https://user-images.githubusercontent.com/25608527/97345049-9c90a280-18af-11eb-969e-719083ecc0de.png)


### MySQL INSERT multiple rows limit
In theory, you can insert any number of rows using a single INSERT statement. However, when MySQL server receives the INSERT statement whose size is bigger than max_allowed_packet, it will issue a packet too large error and terminates the connection.

This statement shows the current value of the max_allowed_packet variable:

`SHOW VARIABLES LIKE 'max_allowed_packet';`

Here is the output on our MySQL database server. Note that the value in your server may be different.

![](https://user-images.githubusercontent.com/25608527/97346451-77049880-18b1-11eb-9d51-0428a99168ac.png)

The number is the Value column is the number of bytes.

To set a new value for the max_allowed_packet variable, you use the following statement:

`SET GLOBAL max_allowed_packet=size;`

where size is an integer that represents the number the maximum allowed packet size in bytes.

Note that the _max_allowed_packet_ has no ___influence on the INSERT INTO .. SELECT statement___. The INSERT INTO .. SELECT statement can insert as many rows as you want.

---
---

## MySQL INSERT INTO SELECT
We learned how to insert one or more rows into a table using the INSERT statement with a list of column values specified in the VALUES clause.
```
INSERT INTO table_name(c1,c2,...)
VALUES(v1,v2,..);
```
Besides using row values in the VALUES clause, you can use the result of a SELECT statement as the data source for the INSERT statement.

The following illustrates the syntax of the INSERT INTO SELECT statement:
```
INSERT INTO table_name(column_list)
SELECT 
   select_list 
FROM 
   another_table
WHERE
   condition;
```
In this syntax, instead of using the VALUES clause, you can use a SELECT statement. The SELECT statement can retrieve data from one or more tables.

The INSERT INTO SELECT statement is very useful when you want to copy data from other tables to a table or to summary data from multiple tables into a table.
MySQL INSERT INTO SELECT example

First, create a new table calledsuppliers :
```
CREATE TABLE suppliers (
    supplierNumber INT AUTO_INCREMENT,
    supplierName VARCHAR(50) NOT NULL,
    phone VARCHAR(50),
    addressLine1 VARCHAR(50),
    addressLine2 VARCHAR(50),
    city VARCHAR(50),
    state VARCHAR(50),
    postalCode VARCHAR(50),
    country VARCHAR(50),
    customerNumber INT,
    PRIMARY KEY (supplierNumber)
);
```

**Note:** that you will learn how to create a new table in the subsequent tutorial. For now, you just need to execute this statement to create the  suppliers table.

Suppose all customers from California, USA become the company’s suppliers. The following query finds all customers who locate in California, USA:
```
SELECT 
    customerNumber,
    customerName,
    phone,
    addressLine1,
    addressLine2,
    city,
    state,
    postalCode,
    country
FROM
    customers
WHERE
    country = 'USA' AND 
    state = 'CA';
```

![](https://user-images.githubusercontent.com/25608527/97347001-32c5c800-18b2-11eb-82d0-ff94b30389f5.png)

**Second,** use the INSERT INTO ... SELECT statement to insert customers who locate in California USA from the  customers table into the  suppliers table:
```
INSERT INTO suppliers (
    supplierName, 
    phone, 
    addressLine1,
    addressLine2,
    city,
    state,
    postalCode,
    country,
    customerNumber
)
SELECT 
    customerName,
    phone,
    addressLine1,
    addressLine2,
    city,
    state ,
    postalCode,
    country,
    customerNumber
FROM 
    customers
WHERE 
    country = 'USA' AND 
    state = 'CA';
```
It returned the following message indicating that 11 rows have been inserted successfully.

`11 row(s) affected Records: 11  Duplicates: 0  Warnings: 0`

**Third,** verify the insert by querying data from the  suppliers table:

`SELECT * FROM suppliers;`

Here is the output:

![](https://user-images.githubusercontent.com/25608527/97347180-6bfe3800-18b2-11eb-8be0-bb35b42b8e3e.png)

---
---

## Using SELECT statement in the VALUES list

**First,** create a new table called stats:
```
CREATE TABLE stats (
    totalProduct INT,
    totalCustomer INT,
    totalOrder INT
);
```

**Second,** use the INSERT statement to insert values that come from the SELECT statements:
```
INSERT INTO stats(totalProduct, totalCustomer, totalOrder)
VALUES(
	(SELECT COUNT(*) FROM products),
	(SELECT COUNT(*) FROM customers),
	(SELECT COUNT(*) FROM orders)
);
```
**In this example:**

- **First,** use the SELECT statements with the COUNT() functions to get the total products, employees, and orders.
- **Second,** use the values returned from the SELECT statement in place of values in the VALUES clause of the INSERT statement.

**Third,** query data from the tablestats:

`SELECT * FROM stats;`

Here is the output:

![](https://user-images.githubusercontent.com/25608527/97347266-8c2df700-18b2-11eb-9efd-6c388699b805.png)


## MySQL INSERT ON DUPLICATE KEY UPDATE
The INSERT ON DUPLICATE KEY UPDATE is a MySQL’s extension to the SQL standard’s INSERT statement.

When you insert a new row into a table if the row causes a duplicate in UNIQUE index or PRIMARY KEY , MySQL will issue an error.

However, if you specify the ON **DUPLICATE KEY UPDATE** option in the INSERT statement, MySQL will update the existing row with the new values instead.

The syntax of INSERT ON DUPLICATE KEY UPDATE statement is as follows:
```
INSERT INTO table (column_list)
VALUES (value_list)
ON DUPLICATE KEY UPDATE
   c1 = v1, 
   c2 = v2,
   ...;
```
The only addition to the INSERT statement is the ON DUPLICATE KEY UPDATE clause where you specify a list of column-value-pair assignments in case of duplicate.

Basically, the statement first tries to insert a new row into the table. If a duplicate error occurs, it will update the existing row with the value specified in the ON DUPLICATE KEY UPDATE clause.

MySQL returns the number of affected-rows based on the action it performs:
```
If the new row is inserted, the number of affected-rows is 1.
If the existing row is updated, the number of affected-rows is 2.
If the existing row is updated using its current values, the number of affected-rows is 0.
```
To use the values from the INSERT clause in the DUPLICATE KEY UPDATE clause, you use the VALUES() function as follows:
```
INSERT INTO table_name(c1)
VALUES(c1)
ON DUPLICATE KEY UPDATE c1 = VALUES(c1) + 1;
```
The statement above sets the value of the c1 to its current value specified by the expression VALUES(c1) plus 1 if there is a duplicate in UNIQUE index or PRIMARY KEY.

MySQL INSERT ON DUPLICATE KEY UPDATE example

Let’s take a look at an example of using the INSERT ON DUPLICATE KEY UPDATE to understand how it works.

First, create a table named devices to store the network devices.
```
CREATE TABLE devices (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```
Next, insert rows into the devices table.
```
INSERT INTO devices(name)
VALUES('Router F1'),('Switch 1'),('Switch 2');
```
Then, query the data from the devices table to verify the insert:
```
SELECT 
    id, 
    name
FROM	
    devices;
```
Here is the output:

![](https://user-images.githubusercontent.com/25608527/97348159-c9df4f80-18b3-11eb-931a-db5e6957a027.png)

Now, we have three rows in the devices table.

After that, insert one more row into the devices table.
```
INSERT INTO 
   devices(name) 
VALUES 
   ('Printer') 
ON DUPLICATE KEY UPDATE name = 'Printer';
```
Here is the output:

![](https://user-images.githubusercontent.com/25608527/97348166-ccda4000-18b3-11eb-9335-b2db0ebb029c.png)

Because there is no duplicate, MySQL inserts a new row into the devices table. The statement above has the same effect as the following statement:
```
INSERT INTO devices(name) 
VALUES ('Printer');
```
Finally, insert a row with a duplicate value in the id column.
```
INSERT INTO devices(id,name) 
VALUES 
   (4,'Printer') 
ON DUPLICATE KEY UPDATE name = 'Central Printer';
```
MySQL issues the following message:

`2 row(s) affected`

Because a row with id 4 already exists in the devices table, the statement updates the name from Printer to Central Printer.
Here is the output:

![](https://user-images.githubusercontent.com/25608527/97348169-ce0b6d00-18b3-11eb-8a1b-e9bb3711e721.png)
