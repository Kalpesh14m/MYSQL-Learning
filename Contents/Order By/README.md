## Introduction to MySQL ORDER BY clause

When you use the [SELECT statement]() to query data from a table, the result set is not sorted. It means that the rows in the result set can be in any order.

To sort the result set, you add the ORDER BY clause to the [SELECT statement](). The following illustrates the syntax of the ORDER BY  clause:

```
SELECT 
   select_list
FROM 
   table_name
ORDER BY 
   column1 [ASC|DESC], 
   column2 [ASC|DESC],
   ...;
```

In this syntax, you specify the one or more columns which you want to sort after the ORDER BY clause.

The **ASC** stands for _ascending_ and the **DESC** stands for _descending_. You use ASC to sort the result set in ascending order and DESC to sort the result set in descending order.

This ORDER BY clause sorts the result set in ascending order:

`ORDER BY column1 ASC;`

And this ORDER BY clause sorts the result set in descending order:

`ORDER BY column1 DESC;`

**By default,** the ORDER BY clause **uses ASC if you don’t explicitly specify any option.**

Therefore, the following clauses are equivalent:

`ORDER BY column1 ASC;`

and

`ORDER BY column1;`

If you want to sort the result set by multiple columns, you specify a comma-separated list of columns in the ORDER BY clause:

```
ORDER BY
   column1,
   column2;
```
It is possible to sort the result by a column in ascending order, and then by another column in descending order:

```
ORDER BY
    column1 ASC,
    column2 DESC;
```

In this case, the ORDER BY clause:

- **First,** sort the result set by the values in the column1 in ascending order.

- **Then,** sort the sorted result set by the values in the column2  in descending order. Note that the order of values in the column1 will not change in this
step, only the order of values in the column2 changes.

**Note that** the ORDER BY clause is always evaluated after the **FROM and [SELECT]() clause.**

![](https://user-images.githubusercontent.com/25608527/100498247-e1e21180-3186-11eb-8c42-07242146c2f2.png)

---

### MySQL ORDER BY examples

We’ll use the customers table from the sample database for the demonstration.

![](https://user-images.githubusercontent.com/25608527/100498246-e1e21180-3186-11eb-9613-e4ca8b984e78.png)


### A) Using MySQL ORDER BY clause to sort values in one column example

The following query uses the ORDER BY clause to sort the customers by the values in the contactLastName column in ascending order.

```
SELECT
	contactLastname,
	contactFirstname
FROM
	customers
ORDER BY
	contactLastname;
```  

![](https://user-images.githubusercontent.com/25608527/100498245-e1497b00-3186-11eb-8a53-709d79dd5f46.png)

If you want to sort customers by the last name in the descending order, you use the DESC after the contactLastname column in the ORDER BY clause as shown in the following query:

```
SELECT
	contactLastname,
	contactFirstname
FROM
	customers
ORDER BY
	contactLastname DESC;
```  

![](https://user-images.githubusercontent.com/25608527/100498244-e0b0e480-3186-11eb-8840-c000f8e28e99.png)


### B) Using MySQL ORDER BY clause to sort values in multiple columns example

If you want to sort the customers by the last name in descending order and then by the first name in ascending order, you specify both  DESC and ASC in the corresponding column as follows:

```
SELECT
	contactLastname,
	contactFirstname
FROM
	customers
ORDER BY
	contactLastname DESC,
	contactFirstname ASC;
```  

![](https://user-images.githubusercontent.com/25608527/100498243-e0184e00-3186-11eb-8937-e219d8540bed.png)

In this example, the ORDER BY  clause sorts the result set by the last name in descending order first and then sorts the sorted result set by the first name in ascending order to produce the final result set.


### C) Using MySQL ORDER BY to sort a result set by an expression example

See the following  orderdetails table from the sample database.

![](https://user-images.githubusercontent.com/25608527/100498242-df7fb780-3186-11eb-8067-cfc6a79b9cd4.png)

The following query selects the order line items from the orderdetails table. It calculates the subtotal for each line item and sorts the result set based on the subtotal.

```
SELECT 
    orderNumber, 
    orderlinenumber, 
    quantityOrdered * priceEach
FROM
    orderdetails
ORDER BY 
   quantityOrdered * priceEach DESC;
```   

![](https://user-images.githubusercontent.com/25608527/100498241-dee72100-3186-11eb-8635-fad3c0ae9aa8.png)

To make the query more readable, you can assign the expression in the SELECT clause a column alias and use that column alias in the ORDER BY clause as shown in the following query:

```
SELECT 
    orderNumber,
    orderLineNumber,
    quantityOrdered * priceEach AS subtotal
FROM
    orderdetails
ORDER BY subtotal DESC;
```

![](https://user-images.githubusercontent.com/25608527/100498240-dee72100-3186-11eb-98af-6a75b631c044.png)

In this example, we used subtotal as the column alias for the expression  quantityOrdered * priceEach and sorted the result set by the subtotal alias.

The column alias can be used in the ORDER BY clause because the SELECT clause is evaluated before the ORDER BY clause. By the time the ORDER BY clause is evaluated, the column alias is accessible.

Using MySQL ORDER BY to sort data using a custom list

The ORDER BY clause allows you to sort data using a custom list by using the [FIELD()]()  function.

See the following orders table from the sample database.

![](https://user-images.githubusercontent.com/25608527/100498239-de4e8a80-3186-11eb-8a4e-690f489c8ce4.png)

Suppose that you want to sort the sales orders based on their statuses in the following order:

- In Process

- On Hold

- Canceled

- Resolved

- Disputed

- Shipped

To do this, you can use the [FIELD() function]() to map each order status to a number and sort the result by the result of the FIELD() function:
```
SELECT 
    orderNumber, 
    status
FROM
    orders
ORDER BY 
    FIELD(status,
        'In Process',
        'On Hold',
        'Cancelled',
        'Resolved',
        'Disputed',
        'Shipped');
```

![](https://user-images.githubusercontent.com/25608527/100498237-dd1d5d80-3186-11eb-8864-8c45936d9409.png        

The following expression:

`FIELD(status, 'In Process', 'On Hold', 'Cancelled', 'Resolved', 'Disputed', 'Shipped');`

returns the index of the status in the list 'In Process', 'On Hold', 'Cancelled', 'Resolved', 'Disputed', 'Shipped'.

For example, if the status is In Process, the function will return 1. If the status is On Hold, the function will return 2, and so on.
