# MySQL Delimiter
When you write SQL statements, you use the semicolon (;) to separate two statements like the following example:

`SELECT * FROM products;`

`SELECT * FROM customers;`

A MySQL client program such as MySQL Workbench or mysql program uses the (;) delimiter to separate statements and executes each statement separately.

A stored procedure, however, consists of multiple statements separated by a semicolon (;).

If you use a MySQL client program to define a stored procedure that contains semicolon characters, the MySQL client program will not treat the whole stored procedure as a single statement, but many statements.

Therefore, you must redefine the delimiter temporarily so that you can pass the whole stored procedure to the server as a single statement.

To redefine the default delimiter, you use the DELIMITER command:

`DELIMITER delimiter_character`

The **delimiter_character** may consist of a ___single character___ or ___multiple characters___ e.g., // or $$. However, you should avoid using the ***backslash (\) because this is the escape character in MySQL.***

For example, this statement **changes the delimiter to //**:

`DELIMITER //`

Once change the delimiter, you can use the new delimiter to end a statement as follows:
```
DELIMITER //

SELECT * FROM customers //

SELECT * FROM products //
```
To **change the delimiter back to semicolon,** you use this statement:

`DELIMITER ;`

Using MySQL DELIMITER for stored procedures

A stored procedure typically contains multiple statements separated by semicolon (;).  To use compile the whole stored procedure as a single compound statement, you need to temporarily change the delimiter from the semicolon (;) to anther delimiters such as $$ or //:
```DELIMITER $$

CREATE PROCEDURE sp_name()
BEGIN
  -- statements
END $$

DELIMITER ;
```
In this code:
**First,** change the default delimiter to $$
**Second,** use (;) in the body of the stored procedure and $$ after the END keyword to end the stored procedure.
**Third,** change the default delimiter back to a semicolon (;)
