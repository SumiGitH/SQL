# SQL

CREATE DATABASE testDB;
SHOW DATABASES;
DROP DATABASE testDB;

CREATE TABLE Persons (
    PersonID int,
    FirstName varchar(255),
    LastName varchar(255) NOT NULL,
    Address varchar(255),
    City varchar(255)
);


SQL COMMANDS

DDL : data definition language. consists of defining, altering and deleting database. it includes Create, Drop, Alter, Truncate, Comment and Rename.
Example: CREATE TABLE Employees (
employee_id INT PRIMARY KEY,
first_name VARCHAR(50),
Last_name VARCHAR(50),
hire_date DATE 
);



DML: INSERT, UPDATE, & DELETE.
Used to manipulate the data.
INSERT INTO employees (first_name, last_name, department) VALUES ('Jane','Smith', 'HR');


TCL: COMMIT, SAVEPOINT, & ROLLBACK: TRANSACTION CONTROL LANGUAGE.
Transactions group a set of tasks into a single execustion unit. Each transaction begins with a specific task and ends when all the tasks in the group are successfully completed. If any of the tasks fail, transaction fails. THerefore, a transaction has only two results: success or failure.
BEGIN TRANSACTION;
UPDATE employees SET department= 'Marketing' WHERE
department = 'Sales';
SAVEPOINT before_update;
UPDATE employees SET department = 'IT' WHERE department = 'HR';
ROLLBACK TO SAVEPOINT before_update;
COMMIT;

DQL: SELECT, FROM, WHERE, GROUP BY, HAVING, DISTINCT, ORDER BY & LIMIT.
Helps inretriveing the data
SELECT first_name, last_name, hire_date
FROM employees
WHERE DEPARTMENT ='Sales'
ORDER BY hire_date DESC;

DCL: GRANT, REVOKE: DATA CONTROL LANGUAGE
Mainly delas with the rights, permissions, and other controls of the database system.
GRANT SELECT, UPDATE ON employeesn TO User_name;

DATA CONSTRAINTS: Use NOT NULL, UNIQUE, PRIMARY KEY and etc to ensure data accuracy.

SQL Datatypes
NUMERIC: INT, DECIMAL, FLOAT, NUMERIC
BINARY: BINARY, BLOB
STRING: CHAR, VARCHAR, TEXT
BOOLEAN: BOOLEAN
DATA/TIME: DATE, TIME, DATETIME
SPECIAL: UUID, AON, XML, JSON

EXACT NUMERIC DATATYPE
BIGINT: Large integer number 
INT: Standard integer values
SAMLLINT: Small integers
TINYINT: Veru=y small integers (0 to 255)
DECIMAL: Excat fixed point numbers
NUMERIC: SImilar DEcimal, used for precision data
Example:
CREATE TABLE Product_Sales (
ProductID INT PRIMARY KEY,
Quantity SMALLINT,
UnitPrice DECIMAL (10,2),
TotalAmount DECIMAL(10,2)
);


APPROXIMATE NUMERIC DATATYPE
FLOAT: Approximate numeric values
REAL: SImilar to FLOAT, But with less precision
EXample:
CREATE TABLE Measurements (
SensorID INT,
Temprature FLOAT,
Humidity REAL
);

CHAR:Fixed-length non-unicode charcaters with a maximum length of 8000 characters
VARCHAR: Variable-length non-unicode characters with a maximum length of 8000 characters.
VARCHAR(MAX): STores variable-length non-unicode data with maximum size of 2 the power 31 - 1 characters
TEXT: STores varibale-length non-unicode data with a maximum size of 2,147,483,647 charcaters.
EXample:
CREATE TABLE Employee_Info (
EmpID INT PRIMARY KEY,
FirstName VARCHAR (50),
LastName CHAR(30),
Bio Nvarchar(max)
);

<img width="800" height="999" alt="image" src="https://github.com/user-attachments/assets/4f88dba4-f82b-4851-b7de-b34aae17498b" />
