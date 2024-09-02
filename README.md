
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

## Modifying Data Using UPDATE
```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
```
UPDATE employees
SET salary = 75000
WHERE employee_id = 6;
```

## Deleting Data Using DELETE
```
DELETE FROM table_name
WHERE condition;
```
```
DELETE FROM employees
WHERE employee_id = 6;
```
## Basic Subqueries in SQL
### 1. Introduction to Subqueries (Nested Queries)
A subquery (also known as a nested query) is a query within another SQL query. The subquery is executed first, and its result is then used by the main query. Subqueries are typically enclosed in parentheses.

Subqueries can be used in various places within a SQL statement, such as in the SELECT list, FROM clause, or WHERE clause.
```
SELECT column1, column2
FROM table1
WHERE column3 = (SELECT column FROM table2 WHERE condition);
```
##### If you want to find all employees who work in the "Sales" department, you can use a subquery:
```
SELECT first_name, last_name
FROM employees
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales');
```
- Explanation: The subquery (SELECT department_id FROM departments WHERE department_name = 'Sales') retrieves the department_id for the Sales department. The main query then selects employees who work in that department.

### 2. Using Subqueries to Filter Data
Subqueries are particularly useful when you need to filter data based on more complex criteria that involve multiple tables or aggregated results.
#### Example 1: Find employees whose salary is above the average salary in their department.
```
SELECT first_name, last_name, salary
FROM employees e
WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);
```
- Explanation: The subquery (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id) calculates the average salary for each department. The main query then selects employees whose salary is higher than this average.
#### Example 2: List departments that have more than one employee.
```
SELECT department_name
FROM departments
WHERE department_id IN (SELECT department_id FROM employees GROUP BY department_id HAVING COUNT(*) > 1);
```
- Explanation: The subquery (SELECT department_id FROM employees GROUP BY department_id HAVING COUNT(*) > 1) finds departments that have more than one employee. The main query retrieves the names of these departments.

# Intermediate Level
### 1. Aggregate function
- COUNT, SUM, AVG, MIN, MAX are aggregate function
```
SELECT COUNT(employee_id) AS total_employees 
FROM employees;
```
##### This(COUNT) query returns the total number of employees.
```
SELECT SUM(salary) AS total_salary
FROM employees;
```
##### This(SUM) query returns the total salary of all employees.
```
SELECT AVG(salary) AS average_salary
FROM employees;
```
##### This(AVG) query returns the average salary of all employees.
```
SELECT MIN(salary) AS lowest_salary
FROM employees;
```
##### This(MIN) query returns the lowest salary among all employees.
```
SELECT MAX(salary) AS highest_salary
FROM employees;
```
##### This(MAX) query returns the highest salary among all employees.

### 2. Grouping Data Using GROUP BY
The GROUP BY clause groups rows that have the same values in specified columns into summary rows, like "total sales per department" or "number of employees per department."
```
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1;
```
##### Example: Group employees by department and calculate the total salary for each department.
```
SELECT department_id, SUM(salary) AS total_salary
FROM employees
GROUP BY department_id;
```
This query groups employees by department_id and calculates the total salary for each department.

### Filtering Grouped Data Using HAVING
The HAVING clause is used to filter groups based on a specified condition. It is similar to the WHERE clause but is applied after the data has been grouped.
```
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
HAVING condition;
```
##### Example: Find departments with a total salary greater than 100,000.
```
SELECT department_id, SUM(salary) AS total_salary
FROM employees
GROUP BY department_id
HAVING SUM(salary) > 100000;
```
This query first groups the data by department_id and calculates the total salary for each group. The HAVING clause then filters these groups to only include those where the total salary exceeds 100,000.






