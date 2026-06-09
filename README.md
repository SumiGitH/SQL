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
