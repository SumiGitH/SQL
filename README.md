<img width="463" height="272" alt="image" src="https://github.com/user-attachments/assets/86f02c4d-64e7-4b8c-adac-fbe81f5e8036" /># SQL

SQL is a standard language for storing, manipulating and retrieving data in databases.

https://datalemur.com/sql-tutorial

What Can SQL do?
SQL can execute queries against a database
SQL can retrieve data from a database
SQL can insert records in a database
SQL can update records in a database
SQL can delete records from a database
SQL can create new databases
SQL can create new tables in a database
SQL can create stored procedures in a database
SQL can create views in a database
SQL can set permissions on tables, procedures, and views


The data in RDBMS is stored in database objects called tables. A table is a collection of related data entries and it consists of columns and rows.


Some of The Most Important SQL Commands
SELECT - extracts data from a database
UPDATE - updates data in a database
DELETE - deletes data from a database
INSERT INTO - inserts new data into a database
CREATE DATABASE - creates a new database
ALTER DATABASE - modifies a database
CREATE TABLE - creates a new table
ALTER TABLE - modifies a table
DROP TABLE - deletes a table
CREATE INDEX - creates an index (search key)
DROP INDEX - deletes an index


Select 
SELECT CustomerName, City FROM Customers;

DISTINCT 
SELECT DISTINCT Country FROM Customers;
SELECT COUNT(DISTINCT Country) FROM Customers;

WHERE
SELECT * FROM Customers
WHERE CustomerID > 80;
Operators used for where clause 
Operator Description 
= Equal 
> Greater than 
< Less than 
>= Greater than or equal 
<= Less than or equal 
<> Not equal. Note: In some versions of SQL this operator may be written as != 
BETWEEN Between a certain range 
LIKE Search for a pattern 
IN To specify multiple possible values for a column


ORDER BY
The ORDER BY keyword sorts the result-set in ascending order (ASC) by default.
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;

WHERE & AND
Select all customers where Country is "Spain" AND CustomerName starts with the letter 'G':
SELECT *
FROM Customers
WHERE Country = 'Spain' AND CustomerName LIKE 'G%';

WHERE OR
Select all Spanish customers that starts with either "G" or "R":

SELECT * FROM Customers
WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%');

Without parenthesis, the SQL above will return all customers from Spain that starts with a "G", plus all customers that starts with an "R", regardless of the country value:

NOT
NOT LIKE
NOT BETWEEN
NOT IN
IS NOT NULL
NOT EXISTS
Select customers that does not start with the letter 'A':

SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'A%';

Select customers that are not from Paris or London:
SELECT * FROM Customers
WHERE City NOT IN ('Paris', 'London');


INSERT INTO
The following SQL inserts a new record in the "Customers" table:

ExampleGet your own SQL Server
INSERT INTO Customers
VALUES ('Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');


CREATE DATABASE testDB;


The DROP DATABASE statement is used to permanently delete an existing SQL database
DROP DATABASE testDB;


Back up 
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak';

Create Table 
CREATE TABLE Persons (
  PersonID int PRIMARY KEY,
  LastName varchar(255) NOT NULL,
  FirstName varchar(255),
  Address varchar(255),
  City varchar(255)
);


Truncate 
TRUNCATE TABLE statement is used to delete all the records in a table, but it keeps the table structure, columns and constraints
TRUNCATE TABLE table_name;



ALTER TABLE operations are:

Add column - Adds a new column to a table
Drop column - Deletes a column in a table
Rename column - Renames a column
Modify column - Changes the data type, size, or constraints of a column
Add constraint - Adds a new constraint
Rename table - Renames a table

ALTER TABLE Customers
DROP COLUMN Email;

ALTER TABLE Customers
MODIFY Email varchar(100) NOT NULL;

ALTER TABLE Members
ADD CONSTRAINT CHK_Age CHECK (Age >= 18);

ALTER TABLE Customers
RENAME TO Clients;

ALTER TABLE Persons
DROP COLUMN DateOfBirth;

SQL Constraints
SQL constraints are rules for data in a table.
Constraints can be specified in two ways:
When a table is created (through the CREATE TABLE statement)
After a table is created (through the ALTER TABLE statement)

SQL Constraint Types
The following constraints are commonly used in SQL:
NOT NULL - Ensures that a column cannot have a NULL value
UNIQUE - Ensures that all values in a column are unique
PRIMARY KEY - Uniquely identifies each row in a table (a combination of a NOT NULL and UNIQUE)
FOREIGN KEY - Establishes a link between data in two tables, and prevents action that will destroy the link between them
CHECK - Ensures that the values in a column satisfies a specific condition
DEFAULT - Sets a default value for a column if no value is specified
CREATE INDEX - Creates indexes on columns to retrieve data from the database faster

CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);

CREATE TABLE Persons (
    ID int NOT NULL UNIQUE,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);









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


DATABASE: Database is a system that allow users to store and organise data.
TYPES
1. Relational Database
2. Non-Relational Databse
   Differences
<img width="463" height="272" alt="image" src="https://github.com/user-attachments/assets/b1cfac9f-01b2-41d8-a575-a9a0b8de13ad" />

Excel Uses: 
- Small amount of data, 
- One time analysis, 
- Quick chart/grpah, 
- Untrained person.

Database Uses: 
- Large Amount of data
- Store real time data from websites/apps
- Easily combine with different datasets
- Automate steps and can re-use
- Easy & Safe access
- Data Integrity: Data integrity refers to the accuracy, completeness, and consistency of data throughout its entire lifecycle. It ensures your information remains fully trustworthy, uncorrupted, and unaltered whether it is being stored, transmitted, or processed. 
- Deep Search Capabilities


To interact with Database you can use: Mysql SQLite, SQL Server, Postgre SQL, Oracle SQL, Snowflake, Amazon Redshift



Database Diagram

<img width="342" height="256" alt="image" src="https://github.com/user-attachments/assets/16235e63-1296-4e39-993d-f342eab434ef" />


