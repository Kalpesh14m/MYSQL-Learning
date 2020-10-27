# MYSQL-Learning

## Database: A database is merely a structured collection of data.
The data relating to each other by nature. Therefore, we use the term relational database.
A table contains columns and rows. It is like a spreadsheet.
A table may relate to another table using a relationship, e.g., one-to-one and one-to-many relationships.

## SQL(structured query language) – the language of the relational database
SQL is the standardized language used to access the database. ANSI/SQL defines the SQL standard.
SQL contains three parts:
  **Data definition language** includes statements that help you define the database and its objects, e.g., tables, views, triggers, stored procedures, etc.
  **Data manipulation language** contains statements that allow you to update and query data.
  **Data control language** allows you to grant the permissions to a user to access specific data in the database.

## What is MySQL
### MySQL? What?
My is the daughter’s name of the MySQL’s co-founder, **Monty Widenius**. The name of MySQL is the combination of My and SQL, MySQL.

MySQL is a database management system that allows you to manage relational databases. It is open source software backed by Oracle. It means you can use MySQL without paying a dime. Also, if you want, you can change its source code to suit your needs. Even though MySQL is open source software, you can buy a commercial license version from Oracle to get premium support services. MySQL is pretty easy to master in comparison with other database software like Oracle Database, or Microsoft SQL Server.

The official way to pronounce MySQL is ***My Ess Que Ell***, not **My Sequel**. However, you can pronounce it whatever you like, who cares?

## Installation Of MySQL (Need to Work...)



### Connect to MySQL server(In Ubuntu | Need to work with MySQL Workbench)
To connect to the MySQL Server, use this command:

`sudo mysql -u root -p`

It will prompt for the password of the root account. You enter the password and press Enter, the following command will show if the password is valid:

`mysql>`

Use the SHOW DATABASES to display all databases in the current server:

`mysql> show databases;`

Here is the output:
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.05 sec)
```



### MySQL Sample Database
We use the classicmodels database as a MySQL sample database to help you work with MySQL quickly and effectively. The classicmodels database is a retailer of scale models of classic cars database. It contains typical business data such as customers, products, sales orders, sales order line items, etc.
Download MySQL Sample Database

### You can download the MySQL sample database via the following link:
### ![classicmodelsDB](https://github.com/Kalpesh14m/MYSQL-Learning/blob/main/Content/mysqlsampledatabase.zip)
The download file is in ZIP format so you need a zip program to unzip it. You can download a free zip program at www.7-zip.org.
After uncompressing the  sampledatabase.zip file, you can load the sample database into MySQL database server by following commands and test it by using the following SQL statements:

#### How to Load the Sample Database into MySQL Server

**Step 1:** Download the ![classicmodels database](https://github.com/Kalpesh14m/MYSQL-Learning/blob/main/Content/mysqlsampledatabase.zip).
**Step 2:** Unzip the downloaded file into a temporary folder. You can use any folder you want. To make it simple, we will unzip the file to the C:\temp  folder.
***Note:*** If you use another operating system such as macOS, Linux, or Unix, please feel free to unzip it to any directory you like.
**Step 3:** Connect to the MySQL server using the mysql client program. The mysql program is located in the bin directory of the MySQL installation folder.

`> mysql -u root -p`
`Enter password: ********`

You will need to enter the password for the root user account to log in.

**Step 4:** Use the source command to load data into the MySQL Server:

`mysql> source c:\temp\mysqlsampledatabase.sql`

**Step 5:** Use the SHOW DATABASES command to list all databases in the current server:

`mysql> show databases;`

The output will look like the following that includes the newly created classicmodels database:
```
+--------------------+
| Database           |
+--------------------+
| classicmodels      |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
```

### To test classicmodelsDB 

`USE classicmodels;`
`SELECT * FROM customers;`

Basically, those statements switch the current database to classicmodels and query data from the customers table. If you see the customer data returned, you have successfully imported the sample database into the MySQL database server.


### MySQL Sample Database Schema

#### The MySQL sample database schema consists of the following tables:

- **Customers:** stores customer’s data.
- **Products:** stores a list of scale model cars.
- **ProductLines:** stores a list of product line categories.
- **Orders:** stores sales orders placed by customers.
- **OrderDetails:** stores sales order line items for each sales order.
- **Payments:** stores payments made by customers based on their accounts.
- **Employees:** stores all employee information as well as the organization structure such as who reports to whom.
- **Offices:** stores sales office data.


![](https://user-images.githubusercontent.com/25608527/97271524-ab973680-1856-11eb-8668-a9c20125a06d.jpg)


### To quit the mysql program, type exit command:

```
mysql> exit
Bye
```


# Table of Content (Index):

| Content | URL |
| :---: | :---: |
| **Database** | ![Database command](https://github.com/Kalpesh14m/MYSQL-Learning/blob/main/Database/README.md) |
| **Select** | ![Select command](https://github.com/Kalpesh14m/MYSQL-Learning/blob/main/Select/README.md) |
| **Insert** | ![Insert command](https://github.com/Kalpesh14m/MYSQL-Learning/blob/main/Insert/README.md) |
| **Update** | ![Update command](https://github.com/Kalpesh14m/MYSQL-Learning/blob/main/Update/README.md) |
| **Delete** | ![Delete command](https://github.com/Kalpesh14m/MYSQL-Learning/blob/main/Delete/README.md) |

