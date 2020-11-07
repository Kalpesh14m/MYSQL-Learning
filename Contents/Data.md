DDL:
	CREATE
		CREATE DATABASE dbLearning;
	
	DROP
		DROP TABLE dept;
	
	ALTER
		ALTER TABLE ORATEST ADD (description VARCHAR(50))
		ALTER TABLE EMP_NEW DROP COLUMN TESTNEW;
		
		ALTER TABLE EMP_NEW ADD PRIMARY KEY (EMPLOYEE_ID)
		ALTER TABLE EMP_NEW DROP PRIMARY KEY;
		
		ALTER TABLE EMP_NEW READ ONLY;
		ALTER TALE EMPREAD WRITE
	
	
	
	TRUNCATE
		TRUNCATE TABLE dept;
	
	RENAME
		ALTER TABLE table_name RENAME TO new_table_name;
	
	
DQL:
	
	SELECT * FROM dept;

	SELECT emp_no, emp_name, city FROM emp;

	SELECT name, age, occupation, coalesce(abc,"TBD") as myData FROM employee_table;

	AND:
		SELECT * FROM table_name WHERE condition1 AND condition2 and ...conditionN;

	OR:
		SELECT * FROM table_name WHERE condition1 OR condition2 OR... conditionN;

	AND OR:
		SELECT * FROM table_name WHERE condition1 AND (condition2 OR condition3);
		
	Wildcard operators:		
		SELECT * FROM Student WHERE NAME LIKE '%T';
SELECT * FROM Student WHERE NAME LIKE 'RAMES_';
SELECT * FROM Student WHERE ADDRESS LIKE '%[^A-C]%';
SELECT * FROM Student WHERE PHONE LIKE '9__5%';
SELECT * FROM Student WHERE ADDRESS LIKE '______';
SELECT DISTINCT * FROM Student WHERE ADDRESS LIKE '%OH%';


	WHERE:
	WHERE Clause is used to filter the records from the table based on the specified condition.
	WHERE Clause can be used without GROUP BY Clause
	WHERE Clause implements in row operations
	WHERE Clause cannot contain aggregate function
	WHERE Clause can be used with SELECT, UPDATE, DELETE statement.
	WHERE Clause is used before GROUP BY Clause
	WHERE Clause is used with single row function like UPPER, LOWER etc.

		SELECT S_Name, Age FROM Student WHERE Age >=18



	HAVING:
	HAVING Clause is used to filter record from the groups based on the specified condition.
	HAVING Clause cannot be used without GROUP BY Clause
	HAVING Clause implements in column operation
	HAVING Clause can contain aggregate function
	HAVING Clause can only be used with SELECT statement.
	HAVING Clause is used after GROUP BY Clause
	HAVING Clause is used with multiple row function like SUM, COUNT etc.

		SELECT Age, COUNT(Roll_No) AS No_of_Students FROM Student GROUP BY Age HAVING COUNT(Roll_No) > 1 

		SELECT column1, function_name(column2)
		FROM table_name
		WHERE condition
		GROUP BY column1, column2
		HAVING condition
		ORDER BY column1, column2;


	ORDER BY:
	Order by statement sort the result-set either in ascending or in descending order.
	While it does not use in CREATE VIEW statement.
	While in select statement, it is always used after the group by keyword.
	Whereas in order by statement, attribute can be under aggregate function.
	Whereas in order by clause, the result-set is sorted based on ascending or descending order.
	While order by clause controls the presentation of columns.

		SELECT column_1, column_2, column_3...........FROM Table_Name ORDER BY column_1, column_2, column_3....... ASC|DESC;

	GROUP BY:	
	Group by statement is used to group the rows that have the same value.
	It may be allowed in CREATE VIEW statement. 
	In select statement, it is always used before the order by keyword.
	Attribute cannot be in the group by statement under aggregate function.
	In group by clause, the tuples are grouped based on the similarity between the attribute values of tuples.
	Group by controls the presentation of tuples(rows).

		SELECT function_Name(column_1), column_2 FROM Table_Name WHERE condition GROUP BY column_1, column_2 ORDER BY column_1, column_2; 

	UNION:
		SELECT ROLL_NO FROM Student UNION SELECT ROLL_NO FROM Student_Details; 
	
	UNION ALL :
		SELECT ROLL_NO FROM Student UNION ALL SELECT ROLL_NO FROM Student_Details; 	

	DISTINCT:
		SELECT DISTINCT column1, column2 FROM table_name 

Sub queries:
	SELECT column1, column2 FROM 
	(SELECT column_x  as C1, column_y FROM table WHERE PREDICATE_X)
	as table2
	WHERE PREDICATE;

DML:
    INSERT
		INSERT INTO dept  (dept_id,dept_name) VALUES (1,"COMP");
		Or 
		INSERT INTO dept VALUES (2,"IT");
		
		COPY table:
		
			INSERT INTO first_table(names_of_columns1) SELECT names_of_columns2 FROM second_table;
			
			INSERT INTO table1 SELECT * FROM table2 WHERE condition;
			
		IGNORE:

			INSERT IGNORE INTO Employee (EmployeeID, Name, City) VALUES (15002, 'Ram', 'Mumbai');

    UPDATE
		UPDATE dept SET dept_name = "CIVIL" WHERE dept_id=2;
		
    DELETE
		DELETE FROM dept where id = 1;


JOIN:
	NATURAL JOIN:
	 	In Natural Join, The resulting table will contain all the attributes of both the tables but keep only one copy of each common column
		In Natural Join, If there is no condition specifies then it returns the rows based on the common column
		SELECT *  FROM Student S NATURAL JOIN Marks M;

    INNER JOIN:
	In Inner Join, The resulting table will contain all the attribute of both the tables including duplicate columns also
	In Inner Join, only those records will return which exists in both the tables	
		SELECT table1.column1,table1.column2,table2.column1,....
		FROM table1 
		INNER JOIN table2
		ON table1.matching_column = table2.matching_column;

    LEFT JOIN:
		SELECT table1.column1,table1.column2,table2.column1,....
		FROM table1 
		LEFT JOIN table2
		ON table1.matching_column = table2.matching_column;

    RIGHT JOIN:
		SELECT table1.column1,table1.column2,table2.column1,....
		FROM table1 
		RIGHT JOIN table2
		ON table1.matching_column = table2.matching_column;

    FULL JOIN:
		SELECT table1.column1,table1.column2,table2.column1,....
		FROM table1 
		FULL JOIN table2
		ON table1.matching_column = table2.matching_column;

	CROSS JOIN/CARTESIAN:
		SELECT table1.column1 , table1.column2, table2.column1...
		FROM table1
		CROSS JOIN table2;

	SELF JOIN:
		SELECT a.coulmn1 , b.column2 FROM table_name a, table_name b WHERE some_condition;


DCL:
    Grant
		GRANT SELECT ON Users TO'Tom'@'localhost;
    
	Revoke
		REVOKE SELECT, UPDATE ON student FROM BCA, MCA;  


TCL
	COMMIT
	ROLLBACK
	SAVEPOINT RollNo


Comments:

	-- another comment

	/* multi line comment
	another comment */

	SELECT * FROM /*  line comments;
	
Aggregate functions:
    These functions are used to do operations from the values of the column and a single value is returned.
        AVG()
			SELECT AVG(column_name) FROM table_name;
        COUNT()
			SELECT COUNT(column_name) FROM table_name;
			SELECT COUNT(DISTINCT AGE) AS NumStudents FROM Students;
		FIRST()
			SELECT FIRST(column_name) FROM table_name;
        LAST()
			SELECT LAST(column_name) FROM table_name;
        MAX()
			SELECT MAX(column_name) FROM table_name;
        MIN()
			SELECT MIN(column_name) FROM table_name;
        SUM()
			SELECT SUM(column_name) FROM table_name;

Scalar functions:
    These functions are based on user input, these too returns single value.
        UCASE()
			SELECT UCASE(column_name) FROM table_name;
        LCASE()
			SELECT LCASE(column_name) FROM table_name;
        MID()
			SELECT MID(column_name,start,length) AS some_name FROM table_name;
        LEN()
			SELECT LENGTH(column_name) FROM table_name;
        ROUND()
			SELECT ROUND(column_name,decimals) FROM table_name; 
        NOW()
			SELECT NOW() FROM table_name;
        FORMAT()
			SELECT NAME, FORMAT(Now(),'YYYY-MM-DD') AS Date FROM Students; 


USE dbLearning;


CREATE TABLE dept
( 
	dept_id int NOT NULL,
	dept_name varchar(50) NOT NULL,
	CONSTRAINT dept_pk PRIMARY KEY (dept_id)
);


CREATE TABLE emp
( 
	emp_no int NOT NULL,
	emp_name varchar(50) NOT NULL,
	dept_id int,
	sal int,
	city varchar(40) default "Mumbai",
	CONSTRAINT emp_pk PRIMARY KEY (emp_no),
	CONSTRAINT dept_fk FOREIGN KEY (dept_id) REFERENCES dept(dept_id) 
);

CREATE TABLE address
(
	add_id int NOT NULL UNIQUE,
	add_type varchar(50) NOT NULL,
	address varchar(50) NOT NULL,
	emp_id int,
	state varchar(40),
	CONSTRAINT add_pk PRIMARY KEY (add_id),
	CONSTRAINT emp_fk FOREIGN KEY (emp_id) REFERENCES emp(emp_no) 
);

SHOW TABLES;

DESC dept;

SELECT * FROM dept;

SELECT emp_no, emp_name, city FROM emp;

select name, age, occupation, coalesce(abc,"TBD") as myData from employee_table;
