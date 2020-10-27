# Operation With Database

### Selecting a MySQL Database Using USE Statement

To select a particular database to work with you issue the USE statement as follows:

`USE database_name;`

In this statement, following the USE keyword is the name of the database that you want to select.

#### USE command to select a database, for example classicmodels:
```
mysql> use classicmodels;
Database changed
```

In this command, we selected the classsicmodels database. If the database exists, MySQL issued the message _“Database changed“_.

#### In case the _database does not exist_, MySQL issued the following error:
```
mysql> use abc;
ERROR 1049 (42000): Unknown database 'abc'
```

#### You can get the name of the currently connected database by using the database() function:
```
mysql> select database();
+---------------+
| database()    |
+---------------+
| classicmodels |
+---------------+
1 row in set (0.00 sec)    
```
#### Finally, to select another database, you just need to issue the USE statement and the new database name, for example:
````
mysql> use tempdb;
Database changed
````

### Selecting a database when you login
If you know which database you want to work with before you log in, you can use the -D flag to specify it as follows:

`MYSQL>mysql -u root -D classicmodels -p`

In this command, we specified the database name classicmodels following the -D flag. Because we used -p flag, MySQL prompted for the password of the root user. You just need to provide the password and press Enter to log in.

#### Once logged in, you can check the current database:
```
> select database();
+---------------+
| database()    |
+---------------+
| classicmodels |
+---------------+
1 row in set (0.00 sec)
```


### MySQL CREATE DATABASE: 
MySQL implements a database as a directory that contains all files which correspond to tables in the database.
To create a new database in MySQL, you use the CREATE DATABASE statement with the following syntax:
```
CREATE DATABASE [IF NOT EXISTS] database_name
[CHARACTER SET charset_name]
[COLLATE collation_name]
```
**First,** specify the database_name following the **CREATE DATABASE** clause. The **database name must be unique** within the MySQL server instance. If you try to create a database with a name that already exists, _MySQL issues an error_.

**Second,** to avoid an error in case you accidentally create a database that __already exists__, you can specify the **IF NOT EXISTS** option. In this case, _MySQL does not issue an error_ but **terminates the CREATE DATABASE statement** instead.

**Third,** specify the character set and collation for the new database at creation time. If you omit the **CHARACTER SET** and **COLLATE clauses**, MySQL uses the _default character set and collation for the new database_.

#### Example CREATE DATABASE command with the database e.g., testdb and press Enter:

```mysql> CREATE DATABASE testdb;
Query OK, 1 row affected (0.12 sec)
```

### Use the SHOW DATABASES to display all databases in the current server:

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

After that, if you want to review the created database, you can use the SHOW CREATE DATABASE command:

`mysql> SHOW CREATE DATABASE testdb;`

![](https://user-images.githubusercontent.com/25608527/97272800-6bd14e80-1858-11eb-9d40-10411da9d43a.jpg)

MySQL returns the database name and the character set and collation of the database.


#### Finally, to access the newly created database, you use the USE database command as follows:

```
mysql> USE testdb;
Database changed
```
Now, you can start creating tables and other databases objects within the  testdb database.



### MySQL DROP DATABASE
The DROP DATABASE statement drops all tables in the database and deletes the database permanently. Therefore, you should be very careful when using this statement.
The following shows the syntax of the DROP DATABASE statement:

`DROP DATABASE [IF EXISTS] database_name;`

In this statement, you specify the _name of the database_ which you want to delete.

If you try to drop a database that does not exist, _MySQL will issue an error_.

To prevent an error from occurring if you delete a database that does not exist, you can use the **IF EXISTS option**. In this case, MySQL terminates the statement without issuing any error.

The DROP DATABASE statement ***returns the number of tables that were deleted***.

In MySQL, the schema is the synonym for the database, therefore, you can use them interchangeably:

`DROP SCHEMA [IF EXISTS] database_name;`

#### DROP DATABASE statement:

```
mysql> DROP DATABASE testdb;
Query OK, 0 rows affected (0.03 sec)
```

MySQL returned zero affected-rows. It means that the testdb database has notable.


## Manage Database in MySQL

### Creating Databases
Before doing anything else with the data, you need to create a database. A database is a container of data. It stores contacts, vendors, customers or any kind of data that you can think of.

In MySQL, a database is a collection of objects that are used to store and manipulate data such as tables, database views, triggers, and stored procedures.

To create a database in MySQL, you use the CREATE DATABASE  statement as follows:

`CREATE DATABASE [IF NOT EXISTS] database_name;`

Let’s examine the CREATE DATABASE  statement in greater detail:

- Followed by the CREATE DATABASE  statement is database name that you want to create. It is recommended that the database name should be as meaningful and descriptive as possible.
- The IF NOT EXISTS  is an optional clause of the statement. The IF NOT EXISTS clause prevents you from an error of creating a new database that already exists in the database server. You cannot have 2 databases with the same name in a MySQL database server.

For example, to create classicmodels database, you can execute the CREATE DATABASE  statement as follows:

`CREATE DATABASE classicmodels;`

After executing this statement, MySQL returns a message to notify whether the new database has been created successfully or not.


### Displaying Databases
The SHOW DATABASES statement lists all databases in the MySQL database server. You can use the SHOW DATABASES statement to check the database that you’ve created or to see all the databases on the database server before you create a new database, for example:

`SHOW DATABASES;`

![](https://user-images.githubusercontent.com/25608527/97274773-1ea2ac00-185b-11eb-9c26-e7caabfd6c70.jpg)

As clearly shown in the output, we have three databases in the MySQL database server. The information_schema  and mysql are the default databases that are available when we install MySQL, and the classicmodels is the new database that we have created.


### Selecting a database to work with
Before working with a particular database, you must tell MySQL which database you want to work with by using the USE  statement.

`USE database_name;`

You can select the classicmodels  sample database using the USE statement as follows:

`USE classicmodels;`

From now, all operations such as querying data, create new tables or calling stored procedures which you perform, will take effects on the current database i.e., classicmodels .


### Removing Databases
Removing database means deleting all the tables contained in the database and the database itself permanently. Therefore, it is very important to execute this query with extra cautions.

To delete a database, you use the DROP DATABASE statement as follows:

`DROP DATABASE [IF EXISTS] database_name;`

Following the DROP DATABASE  clause is the database name that you want to delete. Similar to the CREATE DATABASE  statement, the IF EXISTS  is an optional part of the statement to prevent you from removing a database that does not exist in the database server.

If you want to practice with the DROP DATABASE  statement, you can create a new database, make sure that it is created, and remove it.

Let’s look at the following queries:
```
CREATE DATABASE IF NOT EXISTS tempdb;
SHOW DATABASES;
DROP DATABASE IF EXISTS temp_database;
```
The sequence of three statements is as follows:

- **First,** we created a database named tempdb using the CREATE DATABASE statement.
- **Second,** we displayed all databases using the SHOW DATABASES statement.
- **Third,** we removed the tempdb using the DROP DATABASE statement.
