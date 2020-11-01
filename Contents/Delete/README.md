# MYSQL Delete

To delete data from a table, you use the MySQL DELETE statement. The following illustrates the syntax of the DELETE statement:

```
DELETE FROM table_name
WHERE condition;
```

In this statement:

- **First,** specify the table from which you delete data.

- **Second,** use a condition to specify which rows to delete in the WHERE clause. The DELETE statement will delete rows that match the condition,

**Notice that** the [WHERE clause]() is optional. If you omit the WHERE clause, the DELETE statement will delete all rows in the table.

Besides deleting data from a table, the DELETE statement returns the number of deleted rows.

To delete data from multiple tables using a single DELETE statement, you use the DELETE [JOIN statement]().

To delete all rows in a table without the need of knowing how many rows deleted, you should use the [TRUNCATE TABLE statement]() to get better performance.

For a table that has a foreign key constraint, when you delete rows from the parent table, the rows in the child table will be deleted automatically by using the [ON DELETE CASCADE]() option.

---

### MySQL DELETE examples

We will use the employees table in the [sample database]() for the demonstration.

![](https://user-images.githubusercontent.com/25608527/97775147-63448500-1b84-11eb-9c57-7f65adc9d041.png)

**Note that** once you delete data, it is gone. Later, you will learn how to put the DELETE statement in a transaction so that you can [roll it back]().

### Delete employees whose the officeNumber is 4, you use the DELETE statement with the WHERE clause as shown in the following query:

```
DELETE FROM employees 
WHERE officeCode = 4;
```

### To delete all rows from the employees table, you use the DELETE statement without the WHERE clause as follows:

`DELETE FROM employees;`

All rows in the employees table deleted.

---

### MySQL DELETE and [LIMIT clause]()

If you want to limit the number of rows to delete, use the LIMIT clause as follows:

```
DELETE FROM table_table
LIMIT row_count;
```

**Note that** the order of rows in a table is unspecified, therefore, when you use the LIMIT clause, you should always use the [ORDER BY clause]().

```
DELETE FROM table_name
ORDER BY c1, c2, ...
LIMIT row_count;
```

Consider the following customers table in the sample database:

![](https://user-images.githubusercontent.com/25608527/97775170-a3a40300-1b84-11eb-86b2-a21576ea63e2.png)

**For example,** the following statement sorts customers by customer names alphabetically and deletes the first 10 customers:

```
DELETE FROM customers
ORDER BY customerName
LIMIT 10;
```

Similarly, the following DELETE statement selects customers in France, sorts them by credit limit in from low to high, and deletes the first 5 customers:
```
DELETE FROM customers
WHERE country = 'France'
ORDER BY creditLimit
LIMIT 5;
```

---

## MySQL DELETE JOIN

we learned how to delete rows of multiple tables by using:

- A single DELETE statement on multiple tables.
- A single DELETE statement on multiple related tables which the child table have an [ON DELETE CASCADE]() referential action for the foreign key.

The more flexible way to delete data from multiple tables using INNER JOIN or LEFT JOIN clause with the DELETE statement.


### MySQL DELETE JOIN with [INNER JOIN]()

MySQL also allows you to use the INNER JOIN clause in the DELETE statement to delete rows from a table and the matching rows in another table.

For example, to delete rows from both T1 and T2 tables that meet a specified condition, you use the following statement:

```
DELETE T1, T2
FROM T1
INNER JOIN T2 ON T1.key = T2.key
WHERE condition;
```

**Notice that** you put table names T1 and T2 between the DELETE and FROM keywords. If you omit T1 table, the DELETE statement only deletes rows in T2 table. 

Similarly, if you omitT2 table, the DELETE statement will delete only rows in T1 table.

The expression T1.key = T2.key specifies the condition for matching rows between T1 andT2 tables that will be deleted.

The condition in the  WHERE clause determine rows in the T1 and T2 that will be deleted.

--- 

### MySQL DELETE JOIN with INNER JOIN example

Suppose, we have two tables t1 and t2 with the following structures and data:

```
DROP TABLE IF EXISTS t1, t2;

CREATE TABLE t1 (
    id INT PRIMARY KEY AUTO_INCREMENT
);

CREATE TABLE t2 (
    id VARCHAR(20) PRIMARY KEY,
    ref INT NOT NULL
);

INSERT INTO t1 VALUES (1),(2),(3);

INSERT INTO t2(id,ref) VALUES('A',1),('B',2),('C',3);
```

![](https://user-images.githubusercontent.com/25608527/97778128-01434a00-1b9b-11eb-8d41-b1697893443d.png)

The following statement deletes the row with id 1 in the t1 table and also row with ref 1 in the t2 table using DELETE...INNER JOIN statement:

```
DELETE t1,t2 FROM t1
        INNER JOIN
    t2 ON t2.ref = t1.id 
WHERE
    t1.id = 1;
```

The statement returned the following message:

 `2 row(s) affected`

It indicated that two rows have been deleted.


### MySQL DELETE JOIN with [LEFT JOIN]()

We often use the LEFT JOIN clause in the SELECT statement to find rows in the left table that have or don’t have matching rows in the right table.

We can also use the LEFT JOIN clause in the DELETE statement to delete rows in a table (left table) that does not have matching rows in another table (right table).

The following syntax illustrates how to use DELETE statement with LEFT JOIN clause to delete rows from T1 table that does not have corresponding rows in the T2 table:

```
DELETE T1 
FROM T1
        LEFT JOIN
    T2 ON T1.key = T2.key 
WHERE
    T2.key IS NULL;
```

**Note that** we only put T1 table after the DELETE keyword, not both T1 and T2 tables like we did with the INNER JOIN clause.


### MySQL DELETE JOIN with LEFT JOIN example

See the following customers and orders tables in the sample database:

![](https://user-images.githubusercontent.com/25608527/97778146-26d05380-1b9b-11eb-9560-d3531b25fd14.png)

Each customer has zero or more orders. However, each order belongs to one and only one customer.

We can use DELETE statement with LEFT JOIN clause to clean up our customers master data. The following statement removes customers who have not placed any order:

```
DELETE customers 
FROM customers
        LEFT JOIN
    orders ON customers.customerNumber = orders.customerNumber 
WHERE
    orderNumber IS NULL;
```

We can verify the delete by finding whether  customers who do not have any order exists using the following query:

```
SELECT 
    c.customerNumber, 
    c.customerName, 
    orderNumber
FROM
    customers c
        LEFT JOIN
    orders o ON c.customerNumber = o.customerNumber
WHERE
    orderNumber IS NULL;
```

The query returned an empty result set which is what we expected.

