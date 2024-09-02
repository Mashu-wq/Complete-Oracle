
# Complete Oracle SQL

## Roadmap 
- Basic SQL Queries
- Basic Data Types and Functions
- Simple Joins
- Data Insertion and Modification:
- Basic Subqueries
- Advanced SQL Functions
- Complex Joins and Set Operations
- Advanced Subqueries
- Data Definition Language (DDL)
- Constraints and Indexes
- Views and Sequences
- Transactions and Locks
- Advanced Query Techniques
- Performance Tuning
- PL/SQL Programming
- Advanced PL/SQL
- Working with Large Data Sets
- Advanced Security and Auditing
- Practical Projects

# Beginner Level
## 1. Create A Table
Let's create a simple table called employees with the following columns:

  - employee_id: Number

  - first_name: VARCHAR2(50)

  - last_name: VARCHAR2(50)

  - department: VARCHAR2(50)

  - salary: Number

```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department VARCHAR2(50),
    salary NUMBER
);
```
## 2.Insert Data into the table
Next, let's insert some sample data into the employees table:
```
INSERT INTO employees (employee_id, first_name, last_name, department, salary) 
VALUES (1, 'John', 'Doe', 'Sales', 60000);

INSERT INTO employees (employee_id, first_name, last_name, department, salary) 
VALUES (2, 'Jane', 'Smith', 'HR', 50000);

INSERT INTO employees (employee_id, first_name, last_name, department, salary) 
VALUES (3, 'Mike', 'Johnson', 'IT', 75000);

INSERT INTO employees (employee_id, first_name, last_name, department, salary) 
VALUES (4, 'Emily', 'Davis', 'Sales', 62000);

INSERT INTO employees (employee_id, first_name, last_name, department, salary) 
VALUES (5, 'Michael', 'Brown', 'IT', 68000);
```
## Basic Data Types and Functions
### 1. Common Data Types
- VARCHAR2(A variable-length string data type used to store alphanumeric data);

  Syntax: VARCHAR2(size)
  ```
  first_name VARCHAR2(50);
  ```
  This defines a column first_name that can store up to 50 characters.
- NUMBER (A numeric data type used to store both integers and floating-point numbers)

  Syntax: NUMBER(precision, scale)

  precision: The total number of digits.

  scale: The number of digits to the right of the decimal point.
  ```
  salary NUMBER(8, 2);
  ```
  This defines a salary column that can store up to 8 digits, with 2 digits after the decimal point.
- DATE ( A date data type used to store date and time information)
  ```
  hire_date DATE;
  ```
  This defines a hire_date column to store date values (including time, by default).
### 2.String Functions
- CONCAT(Concatenates (joins) two strings together)

  Syntax: CONCAT(string1, string2)
  ```
  SELECT CONCAT(first_name, last_name) AS full_name FROM employees;
  ```
  This concatenates first_name and last_name into a single string full_name.
- SUBSTR(Extracts a substring from a string)

  Syntax: SUBSTR(string, start_position, length)

  start_position: The position where the substring starts.

  length: The number of characters to extract.

  ```
  SELECT SUBSTR(first_name, 1, 3) AS short_name FROM employees;
  ```
  This extracts the first three characters from first_name.
- LENGTH(Returns the length of a string)

  Syntax: LENGTH(string)
  ```
  SELECT LENGTH(last_name) AS name_length FROM employees;
  ```
  This returns the length of the last_name string.
  



## SELECT Statements: Retrieving Data from a Single Table
The SELECT statement is used to retrieve data from one or more tables. Here’s an example:
```
SELECT column1, column2, column3
FROM table_name;
```
```
//retrieving all the data
SELECT * FROM employees;

SELECT first_name, last_name, email
FROM employees;
```
This query retrieves the first_name, last_name, and email columns from the employees table.

## Filtering Data Using WHERE Clause
The WHERE clause is used to filter records that meet certain conditions.
```
SELECT column1, column2
FROM table_name
WHERE condition;

```
```
SELECT first_name, last_name
FROM employees
WHERE department = 'Sales';

```
This query retrieves the first_name and last_name of employees who work in the Sales department.

## Sorting Data Using ORDER BY Clause
The ORDER BY clause is used to sort the result set by one or more columns.
```
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC|DESC];

```
```
SELECT first_name, last_name, salary
FROM employees
ORDER BY salary DESC;

```
This query retrieves the first_name, last_name, and salary columns from the employees table and sorts the results by salary in descending order.

## Using DISTINCT to Eliminate Duplicates
The DISTINCT keyword is used to remove duplicate records from the result set.
```
SELECT DISTINCT column1, column2
FROM table_name;

```
```
SELECT DISTINCT department
FROM employees;
```
## Simple Joins in SQL
### 1. Understanding and Using INNER JOIN
INNER JOIN is a type of join in SQL that returns rows from two or more tables where the joined columns have matching values. If there are no matches between the tables, those rows are not included in the result.
```
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```
Suppose you have two tables: employees and departments.

## Employees Table

| Column Name   | Data Type      | Description                     |
|---------------|----------------|---------------------------------|
| employee_id   | NUMBER         | Primary key, unique identifier  |
| first_name    | VARCHAR2(50)   | First name of the employee      |
| last_name     | VARCHAR2(50)   | Last name of the employee       |
| department_id | NUMBER         | Foreign key to the departments table |
| salary        | NUMBER         | Employee's salary               |

## Departments Table

| Column Name      | Data Type      | Description                     |
|------------------|----------------|---------------------------------|
| department_id    | NUMBER         | Primary key, unique identifier  |
| department_name  | VARCHAR2(50)   | Name of the department          |

```
CREATE TABLE departments (
    department_id NUMBER PRIMARY KEY,
    department_name VARCHAR2(50) NOT NULL
);
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER,
    salary NUMBER,
    CONSTRAINT fk_department
        FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);

INSERT INTO departments (department_id, department_name) 
VALUES (101, 'Sales');
INSERT INTO departments (department_id, department_name) 
VALUES (102, 'HR');
INSERT INTO departments (department_id, department_name) 
VALUES (103, 'IT');
INSERT INTO employees (employee_id, first_name, last_name, department_id, salary) 
VALUES (1, 'John', 'Doe', 101, 60000);

INSERT INTO employees (employee_id, first_name, last_name, department_id, salary) 
VALUES (2, 'Jane', 'Smith', 102, 50000);
INSERT INTO employees (employee_id, first_name, last_name, department_id, salary) 
VALUES (3, 'Mike', 'Johnson', 101, 75000);
INSERT INTO employees (employee_id, first_name, last_name, department_id, salary) 
VALUES (4, 'Emily', 'Davis', 103, 62000);
INSERT INTO employees (employee_id, first_name, last_name, department_id, salary) 
VALUES (5, 'Michael', 'Brown', 103, 68000);

//To retrieve the employee names along with their department names, you can use an INNER JOIN:

SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.department_id;
```
### 2. Basic Understanding of Table Relationships
Primary Key and Foreign Key relationships are fundamental concepts in relational databases. They establish connections between tables.

- Primary Key:
   - A column or set of columns in a table that uniquely identifies each row.
   - No two rows can have the same primary key value.
  Example: In the departments table, department_id is the primary key because it uniquely identifies each department.
- Foreign Key:
   - A column in one table that refers to the primary key in another table.
   - It establishes a link between the two tables, creating a relationship.
 Example: In the employees table, department_id is a foreign key that references the department_id in the departments table, creating a relationship between employees and departments.
- Table Relationships:
   - One-to-Many Relationship: A single row in one table (e.g., departments) can relate to multiple rows in another table (e.g., employees). For example, one department can have many employees.





