# MYSQL-Learning

## UC1 - Create database for payroll_service
```
create database payroll_service;
```

### see the DB created using show database query
```
show databases;
```

### Go to the database created 
```
use payroll_service;
```

## UC2 - Create Table employee
```
create table employee(
int id primary key,
varchar name(20), 
bigint salary,
date start_date); 
```


