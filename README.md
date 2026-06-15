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
