<a name="update"/>

# MySQL UPDATE

The UPDATE statement updates data in a table. It allows you to change the values in one or more columns of a single row or multiple rows.

The following illustrates the basic syntax of the UPDATE statement:
```
UPDATE [LOW_PRIORITY] [IGNORE] table_name 
SET 
    column_name1 = expr1,
    column_name2 = expr2,
    ...
[WHERE
    condition];
```
In this syntax:

- **First,** specify the name of the table that you want to update data after the UPDATE keyword.
- **Second,** specify which column you want to update and the new value in the SET clause. To update values in multiple columns, you use a list of comma-separated assignments by supplying a value in each column’s assignment in the form of a literal value, an expression, or a subquery.
- **Third,** specify which rows to be updated using a condition in the WHERE clause. The WHERE clause is optional. If you omit it, the UPDATE statement will modify all rows in the table.

**Notice that** the WHERE clause is so important that you should not forget. Sometimes, you may want to update just one row; However, you may forget the WHERE clause and accidentally update all rows of the table.

### MySQL supports two modifiers in the UPDATE statement.
The **LOW_PRIORITY modifier** instructs the UPDATE statement to delay the update until there is no connection reading data from the table. The LOW_PRIORITY takes effect for the storage engines that use table-level locking only such as MyISAM, MERGE, and MEMORY.
The **IGNORE modifier** enables the UPDATE statement to continue updating rows even if errors occurred. The rows that cause errors such as duplicate-key conflicts are not updated.

MySQL UPDATE examples

Let’s practice the UPDATE statement.

---

### 1) Using MySQL UPDATE to modify values in a single column example

See the following employees table from the sample database.

![](https://user-images.githubusercontent.com/25608527/97360405-2cd8e280-18c4-11eb-9f96-0376d0556223.png)


In this example, we will update the email of Mary Patterson to the new email mary.patterso@classicmodelcars.com.

#### **First,** find Mary’s email from the employees table using the following SELECT statement:
```
SELECT 
    firstname, 
    lastname, 
    email
FROM
    employees
WHERE
    employeeNumber = 1056;
```
![](https://user-images.githubusercontent.com/25608527/97360406-2e0a0f80-18c4-11eb-8d73-0cd12df5d557.png)


#### **Second,** update the email address of Mary to the new email mary.patterson@classicmodelcars.com :
```
UPDATE employees 
SET 
    email = 'mary.patterson@classicmodelcars.com'
WHERE
    employeeNumber = 1056;
```
MySQL issued the number of rows affected:

`1 row(s) affected`

In this UPDATE statement:

The WHERE clause specifies the row with employee number 1056 will be updated.
The SET clause sets the value of the email column to the new email.


#### **Third,**  execute the SELECT statement again to verify the change:
```
SELECT 
    firstname, 
    lastname, 
    email
FROM
    employees
WHERE
    employeeNumber = 1056;
```    
  
![](https://user-images.githubusercontent.com/25608527/97360407-2ea2a600-18c4-11eb-80ec-2e70d5ca67c4.png)

---

### 2) Using MySQL UPDATE to modify values in multiple columns
To update values in the multiple columns, you need to specify the assignments in the SET clause. For example, the following statement updates both last name and email columns of employee number 1056:
```
UPDATE employees 
SET 
    lastname = 'Hill',
    email = 'mary.hill@classicmodelcars.com'
WHERE
    employeeNumber = 1056;
```
Let’s verify the changes:
```
SELECT 
    firstname, 
    lastname, 
    email
FROM
    employees
WHERE
    employeeNumber = 1056;
```
![](https://user-images.githubusercontent.com/25608527/97360414-306c6980-18c4-11eb-8196-3480bd14b442.png)
      
---

### 3) Using MySQL UPDATE to replace string example
The following example updates the domain parts of emails of all Sales Reps with office code 6:
```
UPDATE employees
SET email = REPLACE(email,'@classicmodelcars.com','@mysqltutorial.org')
WHERE
   jobTitle = 'Sales Rep' AND
   officeCode = 6;
```

In this example, the REPLACE() function replaces @classicmodelcars.com in the email column with @mysqltutorial.org.

---

### 4) Using MySQL UPDATE to update rows returned by a SELECT statement example
You can supply the values for the SET clause from a SELECT statement that queries data from other tables.

For example, in the customers table, some customers do not have any sale representative. The value of the column saleRepEmployeeNumber is NULL as follows:
```
SELECT 
    customername, 
    salesRepEmployeeNumber
FROM
    customers
WHERE
    salesRepEmployeeNumber IS NULL;
```
![](https://user-images.githubusercontent.com/25608527/97360418-31050000-18c4-11eb-8861-fcfbae51b553.png)
  
We can take a sale representative and update for those customers.

To do this, we can select a random employee whose job title is Sales Rep from the  employees table and update it for the  employees table.

This query selects a random employee from the table employees whose job title is the Sales Rep.
```
SELECT 
    employeeNumber
FROM
    employees
WHERE
    jobtitle = 'Sales Rep'
ORDER BY RAND()
LIMIT 1;
```
To update the sales representative employee number  column in the customers table, we place the query above in the SET clause of the UPDATE statement as follows:
```
UPDATE customers 
SET 
    salesRepEmployeeNumber = (SELECT 
            employeeNumber
        FROM
            employees
        WHERE
            jobtitle = 'Sales Rep'
        ORDER BY RAND()
        LIMIT 1)
WHERE
    salesRepEmployeeNumber IS NULL;
```
If you query data from the  employees table, you will see that every customer has a sales representative. In other words, the following query returns no row.
```
SELECT 
     salesRepEmployeeNumber
FROM
    customers
WHERE
    salesRepEmployeeNumber IS NULL;
```

---

## MySQL UPDATE JOIN

You often use [joins]() to query rows from a table that have (in the case of INNER JOIN) or may not have (in the case of [LEFT JOIN]()) matching rows in another table. In MySQL, you can use the JOIN clauses in the [UPDATE statement](#update) to perform the cross-table update.

The syntax of the MySQL UPDATE JOIN  is as follows:

```
UPDATE T1, T2,
[INNER JOIN | LEFT JOIN] T1 ON T1.C1 = T2. C1
SET T1.C2 = T2.C2, 
    T2.C3 = expr
WHERE condition
```

### Let’s examine the MySQL UPDATE JOIN  syntax in greater detail:

**First,** specify the main table ( T1 ) and the table that you want the main table to join to ( T2 ) after the UPDATE clause. ***Notice that*** you must specify at least one table after the UPDATE  clause. The data in the table that is not specified after the UPDATE  clause will not be updated.

**Next,** specify a kind of join you want to use i.e., either INNER JOIN  or LEFT JOIN  and a join predicate. The JOIN clause must appear right after the UPDATE clause.

**Then,** assign new values to the columns in T1 and/or T2 tables that you want to update.

**After that,** specify a condition in the WHERE clause to limit rows to rows for updating.

If you follow the [UPDATE statement](#update), you will notice that there is another way to update data cross-table using the following syntax:

```
UPDATE T1, T2
SET T1.c2 = T2.c2,
      T2.c3 = expr
WHERE T1.c1 = T2.c1 AND condition
```

This UPDATE  statement works the same as UPDATE JOIN  with an implicit [INNER JOIN  clause](). It means you can rewrite the above statement as follows:

```
UPDATE T1,T2
INNER JOIN T2 ON T1.C1 = T2.C1
SET T1.C2 = T2.C2,
      T2.C3 = expr
WHERE condition
```
Let’s take a look at some examples of using the UPDATE JOIN  statement to having a better understanding.


### MySQL UPDATE JOIN examples

We are going to use a new sample database named empdb in for demonstration. This sample database consists of two tables:

    - The  employees table stores employee data with employee id, name, performance, and salary.
    - The merits table stores employee performance and merit’s percentage.

The following statements create and load data in the empdb sample database:

```
CREATE DATABASE IF NOT EXISTS empdb;

USE empdb;
```

**-- create tables**

```
CREATE TABLE merits (
    performance INT(11) NOT NULL,
    percentage FLOAT NOT NULL,
    PRIMARY KEY (performance)
);

CREATE TABLE employees (
    emp_id INT(11) NOT NULL AUTO_INCREMENT,
    emp_name VARCHAR(255) NOT NULL,
    performance INT(11) DEFAULT NULL,
    salary FLOAT DEFAULT NULL,
    PRIMARY KEY (emp_id),
    CONSTRAINT fk_performance FOREIGN KEY (performance)
        REFERENCES merits (performance)
);
```

**-- insert data for merits table**

```INSERT INTO merits(performance,percentage)
VALUES(1,0),
      (2,0.01),
      (3,0.03),
      (4,0.05),
      (5,0.08);
-- insert data for employees table

INSERT INTO employees(emp_name,performance,salary)      
VALUES('Mary Doe', 1, 50000),
      ('Cindy Smith', 3, 65000),
      ('Sue Greenspan', 4, 75000),
      ('Grace Dell', 5, 125000),
      ('Nancy Johnson', 3, 85000),
      ('John Doe', 2, 45000),
      ('Lily Bush', 3, 55000);
```

MySQL UPDATE JOIN example with [INNER JOIN clause]()

Suppose you want to adjust the salary of employees based on their performance.

The merit’s percentages are stored in the merits table, therefore, you have to use the UPDATE INNER JOIN statement to adjust the salary of employees in the employees  table based on the percentage stored in the merits table.

The link between the employees and merit tables is the performance  field. See the following query:

```
UPDATE employees
        INNER JOIN
    merits ON employees.performance = merits.performance 
SET 
    salary = salary + salary * percentage;
```

![](https://user-images.githubusercontent.com/25608527/97774517-85d39f80-1b7e-11eb-8ce1-dd1c60e9668b.png)

How the query works.

We specify only the employees table after UPDATE clause because we want to update data in the  employees table only.

For each row in the employees table, the query checks the value in the performance column against the value in the performance column in the merits table. If it finds a match, it gets the percentage in the merits  table and updates the salary column in the employees  table.

Because we omit the WHERE clause in the UPDATE statement, all the records in the employees  table get updated.

### MySQL UPDATE JOIN example with LEFT JOIN

Suppose the company hires two more employees:

```
INSERT INTO employees(emp_name,performance,salary)
VALUES('Jack William',NULL,43000),
      ('Ricky Bond',NULL,52000);
```

Because these employees are new hires so their performance data is not available or NULL .

![](https://user-images.githubusercontent.com/25608527/97774596-32ae1c80-1b7f-11eb-87c4-16f0361eb441.png)

To increase the salary for new hires, you cannot use the UPDATE INNER JOIN  statement because their performance data is not available in the merit  table. This is why the UPDATE [LEFT JOIN]() comes to the rescue.

The UPDATE LEFT JOIN  statement basically updates a row in a table when it does not have a corresponding row in another table.

For example, you can increase the salary for a new hire by 1.5%  using the following statement:

```
UPDATE employees
        LEFT JOIN
    merits ON employees.performance = merits.performance 
SET 
    salary = salary + salary * 0.015
WHERE
    merits.percentage IS NULL;
```

![](https://user-images.githubusercontent.com/25608527/97774641-a0f2df00-1b7f-11eb-8138-e7612a71de21.png)
