
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

### 3.Filtering Grouped Data Using HAVING
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

## Complex Joins and Set Operations in SQL
### 1. Understanding LEFT JOIN, RIGHT JOIN, and FULL OUTER JOIN
Joins are used to combine rows from two or more tables based on a related column. While INNER JOIN only returns rows with matching values in both tables, complex joins like LEFT JOIN, RIGHT JOIN, and FULL OUTER JOIN allow you to include non-matching rows as well.

- LEFT JOIN (or LEFT OUTER JOIN):
   - Description: Returns all rows from the left table and the matched rows from the right table. If there is no match, NULL values are returned for columns from the right table.
```
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
##### Example:
```
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.department_id;
```
- RIGHT JOIN (or RIGHT OUTER JOIN):
   - Description: Returns all rows from the right table and the matched rows from the left table. If there is no match, NULL values are returned for columns from the left table.
```
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.department_id;
```
- FULL OUTER JOIN:
   - Description: Returns all rows when there is a match in either the left or right table. If there is no match, NULL values are returned for columns from the non-matching table.
```
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
FULL OUTER JOIN departments
ON employees.department_id = departments.department_id;
```
### 2. Using UNION, INTERSECT, and MINUS to Combine Multiple Result Sets
Set operations allow you to combine the results of two or more SELECT queries. The key set operations are UNION, INTERSECT, and MINUS.
- UNION:
  - Description: Combines the results of two or more SELECT queries, eliminating duplicate rows. The result set includes all rows from both queries.
```
SELECT columns FROM table1
UNION
SELECT columns FROM table2;
```
```
SELECT first_name, last_name FROM employees
UNION
SELECT first_name, last_name FROM customers;
```
- INTERSECT:
   - Description: Returns only the rows that are common to both SELECT queries.
```
SELECT columns FROM table1
INTERSECT
SELECT columns FROM table2;
```
```
SELECT first_name, last_name FROM employees
INTERSECT
SELECT first_name, last_name FROM customers;
```
- MINUS:
   - Description: Returns the rows from the first SELECT query that are not in the result of the second SELECT query.
```
SELECT columns FROM table1
MINUS
SELECT columns FROM table2;
```
```
SELECT first_name, last_name FROM employees
MINUS
SELECT first_name, last_name FROM customers;
```
## Advanced Subqueries in SQL
### 1. Correlated Subqueries
A correlated subquery is a subquery that references columns from the outer query. Unlike a regular subquery, a correlated subquery is executed once for each row processed by the outer query. This type of subquery is useful when the subquery needs to be evaluated for each row in the outer query.
```
SELECT column1, column2
FROM table1 AS t1
WHERE columnX = (SELECT aggregate_function(columnY)
                FROM table2 AS t2
                WHERE t2.columnZ = t1.columnZ);
```
##### Example: Find all employees whose salary is above the average salary of their department.
```
SELECT first_name, last_name, salary
FROM employees e
WHERE salary > (SELECT AVG(salary)
                FROM employees
                WHERE department_id = e.department_id);
```
- Explanation: The subquery calculates the average salary for the department of each employee. The outer query then selects only those employees whose salary is greater than this department average.
### 2. Using Subqueries in SELECT and FROM Clauses
Subqueries can also be used within the SELECT and FROM clauses to perform complex operations.
- #### Subquery in the SELECT Clause:
##### Example: Display the name of each employee along with the total salary of their department.
```
SELECT first_name, last_name, 
       (SELECT SUM(salary)
        FROM employees
        WHERE department_id = e.department_id) AS department_total_salary
FROM employees e;
```
 - Explanation: The subquery calculates the total salary for the department of each employee and displays it alongside the employee's name.
- #### Subquery in the FROM Clause:
##### Example: Find the average salary of all departments and display it alongside the department name.
```
SELECT d.department_name, avg_dept_salary
FROM departments d
JOIN (SELECT department_id, AVG(salary) AS avg_dept_salary
      FROM employees
      GROUP BY department_id) e_avg
ON d.department_id = e_avg.department_id;
```
- The subquery in the FROM clause calculates the average salary for each department. The main query then joins this result with the departments table to display the department names alongside their average salaries.
### 3. EXISTS and NOT EXISTS in Subqueries
The EXISTS and NOT EXISTS operators are used to test for the existence of rows returned by a subquery. These operators are typically used in the WHERE clause.
- #### EXISTS:
  - Description: Returns TRUE if the subquery returns one or more rows. It is often used to check if a certain condition is met.
```
SELECT columns
FROM table1
WHERE EXISTS (SELECT 1
              FROM table2
              WHERE condition);
```
##### Example: Find all departments that have at least one employee.
```
SELECT department_name
FROM departments d
WHERE EXISTS (SELECT 1
              FROM employees e
              WHERE e.department_id = d.department_id);
```
 - Explanation: The subquery checks whether there is at least one employee in each department. The outer query returns the department names where this condition is true.
- #### NOT EXISTS:
  - Description: Returns TRUE if the subquery returns no rows. It is often used to find records that do not have a corresponding entry in another table.
```
SELECT columns
FROM table1
WHERE NOT EXISTS (SELECT 1
                  FROM table2
                  WHERE condition);
```
##### Example: Find all departments that do not have any employees.
```
SELECT department_name
FROM departments d
WHERE NOT EXISTS (SELECT 1
                  FROM employees e
                  WHERE e.department_id = d.department_id);
```
 - Explanation: The subquery checks whether there are no employees in each department. The outer query returns the department names where this condition is true.
## Data Definition Language (DDL) in SQL
DDL (Data Definition Language) statements are used to define and manage database structures such as tables, indexes, and constraints. The most common DDL commands are CREATE, ALTER, and DROP.
### 1. Creating Tables Using CREATE TABLE
```
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ...
);
```
##### Example: Create a table named employees with columns for employee_id, first_name, last_name, department_id, and salary.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50) NOT NULL,
    last_name VARCHAR2(50) NOT NULL,
    department_id NUMBER,
    salary NUMBER
);
```
### 2. Modifying Table Structures Using ALTER TABLE
The ALTER TABLE statement is used to modify an existing table's structure. You can add, modify, or drop columns and constraints.
```
ALTER TABLE table_name
ADD column_name datatype constraint;

ALTER TABLE table_name
MODIFY column_name datatype constraint;

ALTER TABLE table_name
DROP COLUMN column_name;
```
##### Examples: 
- Adding a New Column: Add a hire_date column to the employees table.
```
ALTER TABLE employees
ADD hire_date DATE;
```
- Modifying an Existing Column: Change the data type of the salary column to allow for larger numbers.
```
ALTER TABLE employees
MODIFY salary NUMBER(10, 2);
```
- Dropping a Column: Remove the department_id column from the employees table.
```
ALTER TABLE employees
DROP COLUMN department_id;
```
### 3. Dropping Tables and Other Database Objects Using DROP
The DROP statement is used to delete entire tables or other database objects such as views, indexes, or databases. Once a table is dropped, all the data in the table is lost permanently.
```
DROP TABLE table_name;

DROP VIEW view_name;

DROP INDEX index_name;
```
##### Example:
- Dropping a Table: Delete the employees table from the database.
```
DROP TABLE employees;
```
- Dropping a View: Remove a view named employee_view.
```
DROP VIEW employee_view;
```
- Dropping an Index: Delete an index named emp_salary_idx.
```
DROP INDEX emp_salary_idx;
```
## Data Manipulation Language (DML) in SQL
Data Manipulation Language (DML) consists of SQL commands that are used to manage and manipulate data within existing database tables. The most common DML commands are INSERT, UPDATE, DELETE, and SELECT.

## Constraints and Indexes in SQL
### 1. Implementing Constraints
Constraints are rules enforced on data columns in a database table to ensure data integrity and accuracy. There are several types of constraints, each serving a specific purpose.
- #### Primary Key Constraint:
  - Purpose: Uniquely identifies each record in a table. A primary key column cannot contain NULL values and must contain unique values.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50)
);
```
- #### Foreign Key Constraint(Self-Referencing):
  - Purpose: Establishes a relationship between two tables by linking a column in one table to the primary key of another table. It ensures referential integrity.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER,
    CONSTRAINT fk_department
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```
- #### Unique Constraint:
  - Purpose: Ensures that all values in a column are unique, preventing duplicate entries.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    email VARCHAR2(100) UNIQUE,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50)
);
```
- #### Check Constraint:
  - Purpose: Ensures that all values in a column satisfy a specific condition.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    salary NUMBER,
    CONSTRAINT chk_salary CHECK (salary > 0)
);
```
- #### Not Null Constraint:
  - Purpose: Ensures that a column cannot contain NULL values.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50) NOT NULL,
    last_name VARCHAR2(50) NOT NULL
);
```
- #### Default Constraint
  - Purpose: The DEFAULT constraint automatically assigns a default value to a column if no value is specified during the insertion of a new row.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    hire_date DATE DEFAULT SYSDATE,
    first_name VARCHAR2(50)
);
```
### 2. Understanding and Creating Indexes
Indexes are database objects that improve the speed of data retrieval operations on a table by creating a data structure (usually a B-tree) that allows for fast searching.
- Purpose of Indexes:
  - Improve Query Performance: Indexes speed up the retrieval of rows from a table by reducing the amount of data that needs to be scanned.
  - Used in WHERE Clauses: Indexes are especially useful when filtering data using WHERE clauses or when sorting data using ORDER BY.
- #### Creating Index
```
CREATE INDEX index_name
ON table_name (column1, column2, ...);
```
##### Example: Create an index on the last_name column in the employees table.
```
CREATE INDEX idx_last_name
ON employees (last_name);
```
  - Explanation: This index, named idx_last_name, will improve the performance of queries that filter or sort based on the last_name column.
- #### Types of Indexes:
  - ##### Single-Column Index: An index on a single column.
```
 CREATE INDEX idx_first_name
ON employees (first_name);
```
 - ##### Composite Index: An index on multiple columns.
```
CREATE INDEX idx_name_salary
ON employees (last_name, salary);
```
 - #### Unique Index: An index that ensures all values in the indexed column(s) are unique. Often created automatically when a UNIQUE or PRIMARY KEY constraint is applied.
```
CREATE UNIQUE INDEX idx_unique_email
ON employees (email);
```
 - Considerations When Using Indexes:
   - Disk Space: Indexes require additional storage space.
   - Performance Trade-offs: While indexes speed up data retrieval, they can slow down INSERT, UPDATE, and DELETE operations because the index must also be updated.
   - Selective Use: Indexes should be created on columns that are frequently used in search conditions or joins, but not on every column.
## Set Membership Operators in SQL: SOME, ALL, and UNIQUE
These operators are used to compare a value against a set of values, often returned by a subquery. They allow you to perform conditional checks across multiple values efficiently.
### 1. SOME (or ANY)
The SOME operator (also known as ANY in many SQL dialects) is used to compare a value to each value in a list or a subquery. It returns TRUE if the comparison is true for at least one value in the set.
```
expression operator SOME (subquery)
```
- #### Operator: Can be =, !=, >, <, >=, or <=.
 - ##### Example: Find employees who earn more than some employees in the Sales department.
```
SELECT first_name, last_name, salary
FROM employees
WHERE salary > SOME (SELECT salary FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales'));
```
- Explanation: This query returns employees whose salary is greater than the salary of at least one employee in the Sales department.
### 2. ALL
The ALL operator is used to compare a value to all values in a list or a subquery. It returns TRUE if the comparison is true for all values in the set.
```
expression operator ALL (subquery)
```
- #### Operator: Can be =, !=, >, <, >=, or <=.
  - ##### Example: Find employees who earn more than all employees in the Sales department.
```
SELECT first_name, last_name, salary
FROM employees
WHERE salary > ALL (SELECT salary FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales'));
```
- Explanation: This query returns employees whose salary is greater than the salary of every employee in the Sales department.
### 3. UNIQUE
The UNIQUE operator is used to check whether the results of a subquery contain any duplicate values. It returns TRUE if all the values in the result set are unique.
```
SELECT column_name
FROM table_name
WHERE UNIQUE (subquery);
```
- Note: The UNIQUE keyword is not supported in all SQL implementations; it is often replaced by specific constraints or checks depending on the SQL dialect (for example, using the DISTINCT keyword or enforcing unique constraints).
- ##### Example: Let's say we want to ensure there is only one unique salary value in a specific department.
```
SELECT salary
FROM employees
WHERE UNIQUE (SELECT salary FROM employees WHERE department_id = 101);
```
- SOME (or ANY) is used to check if a condition is true for at least one value in a set.
- ALL is used to check if a condition is true for all values in a set.
- UNIQUE is used to ensure that all values in a result set are distinct, although it may not be supported in all SQL dialects.
## Set Membership in SQL: AND, OR, and NOT
Set membership operations in SQL involve using logical operators like AND, OR, and NOT to filter query results based on multiple conditions. These operators help define whether rows meet certain criteria or not.
### 1. Using AND
The AND operator is used to combine two or more conditions in a SQL query. Rows are included in the result set only if all the conditions are true.
```
SELECT columns
FROM table_name
WHERE condition1 AND condition2 AND ...;
```
- ##### Example: Retrieve employees who work in the Sales department and earn more than 50,000.
```
SELECT first_name, last_name, department_id, salary
FROM employees
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales')
  AND salary > 50000;
```
### 2. Using OR
The OR operator is used to combine two or more conditions. Rows are included in the result set if at least one of the conditions is true.
```
SELECT columns
FROM table_name
WHERE condition1 OR condition2 OR ...;
```
##### Example: Retrieve employees who work in the Sales department or earn more than 70,000.
```
SELECT first_name, last_name, department_id, salary
FROM employees
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales')
  OR salary > 70000;
```
### 3. Using NOT
The NOT operator is used to negate a condition. Rows are included in the result set if the specified condition is false.
```
SELECT columns
FROM table_name
WHERE NOT condition;
```
##### Example: Retrieve employees who do not work in the Sales department.
```
SELECT first_name, last_name, department_id, salary
FROM employees
WHERE NOT department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales');
```
### Combining AND, OR, and NOT
- ##### Example: Retrieve employees who work in the Sales department or in any department but earn less than 50,000.
```
SELECT first_name, last_name, department_id, salary
FROM employees
WHERE (department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales')
  OR salary < 50000)
  AND NOT department_id = (SELECT department_id FROM departments WHERE department_name = 'HR');
```
## Wildcards in SQL
In SQL, wildcards are special characters used with the LIKE operator to search for patterns within text data. The two most common wildcards are % and _.
### 1. Percent (%) Wildcard
The % wildcard matches any sequence of characters, including an empty string. It's used when you want to find strings that contain a specific sequence of characters, regardless of what comes before or after that sequence.
```
SELECT column_name
FROM table_name
WHERE column_name LIKE 'pattern%';
```
- ##### Examples:
  - Find names that start with 'J':
```
SELECT first_name
FROM employees
WHERE first_name LIKE 'J%';
```
   - Find names that contain 'ohn':
```
SELECT first_name
FROM employees
WHERE first_name LIKE '%ohn%';
```
   - Find names that end with 'n':
```
SELECT first_name
FROM employees
WHERE first_name LIKE '%n';
```
### 2. Underscore (_) Wildcard
The _ wildcard matches any single character. It's used when you want to find strings that match a specific pattern, but with exactly one character in a particular position.
```
SELECT column_name
FROM table_name
WHERE column_name LIKE 'pattern_';
```
- ##### Examples:
  - Find names that are exactly four characters long:
```
SELECT first_name
FROM employees
WHERE first_name LIKE '____';
```
   - Find names where the second letter is 'a':
```
SELECT first_name
FROM employees
WHERE first_name LIKE '_a%';
```
- Explanation: This query returns all first_name values where the second character is 'a'. The first character can be anything, and the % allows for any number of characters following the 'a'.
  - Find names that start with 'J' and have exactly three characters:
```
SELECT first_name
FROM employees
WHERE first_name LIKE 'J__';
```
### Combining % and _ Wildcards
You can combine % and _ in a single LIKE pattern to create more complex search criteria.
```
SELECT first_name
FROM employees
WHERE first_name LIKE 'J_n%';
```
- Explanation: This query returns all first_name values that start with 'J', have 'n' as the third character, and can have any number of characters after that.

# Advance Level
## Cascading Actions in Referential Integrity
Cascading actions are mechanisms used in relational databases to maintain referential integrity between tables when performing operations such as DELETE or UPDATE. These actions define what should happen to related rows in a child table when a row in the parent table is updated or deleted.
### Referential Integrity
Referential integrity ensures that relationships between tables remain consistent. Specifically, it ensures that a foreign key in a child table always references a valid row in the parent table.
- Parent Table: The table that is referenced by a foreign key.
- Child Table: The table that contains the foreign key referencing the parent table.
## Cascading Actions
When defining foreign keys, you can specify cascading actions that dictate what happens when the parent key is updated or deleted. The most common cascading actions are CASCADE, SET NULL, SET DEFAULT, and NO ACTION (or RESTRICT).
### 1. ON DELETE CASCADE
- Purpose: Automatically deletes the corresponding rows in the child table when a row in the parent table is deleted.
  - Example:
```
CREATE TABLE departments (
    department_id NUMBER PRIMARY KEY,
    department_name VARCHAR2(50)
);

CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER,
    FOREIGN KEY (department_id) REFERENCES departments(department_id) ON DELETE CASCADE
);
```
- Explanation: In this example, if a row in the departments table is deleted, all rows in the employees table that reference that department_id will also be deleted.
### 2. ON UPDATE CASCADE
- Purpose: Automatically updates the corresponding foreign key values in the child table when the primary key value in the parent table is updated.
  - Example:
```
CREATE TABLE departments (
    department_id NUMBER PRIMARY KEY,
    department_name VARCHAR2(50)
);

CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER,
    FOREIGN KEY (department_id) REFERENCES departments(department_id) ON UPDATE CASCADE
);
```
- Explanation: If the department_id in the departments table is updated, the corresponding department_id values in the employees table will also be updated.
### 3. ON DELETE SET NULL
- Purpose: Sets the foreign key column to NULL in the child table when the corresponding row in the parent table is deleted.
  - Example:
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER,
    FOREIGN KEY (department_id) REFERENCES departments(department_id) ON DELETE SET NULL
);
```
- Explanation: If a row in the departments table is deleted, the department_id in the employees table is set to NULL for all related employees.
### 4. ON UPDATE SET NULL
- Purpose: Sets the foreign key column to NULL in the child table when the corresponding primary key in the parent table is updated.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER,
    FOREIGN KEY (department_id) REFERENCES departments(department_id) ON UPDATE SET NULL
);
```
- Explanation: If the department_id in the departments table is updated, the corresponding department_id in the employees table is set to NULL.
### 5. ON DELETE SET DEFAULT
- Purpose: Sets the foreign key column to its default value when the corresponding row in the parent table is deleted.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER DEFAULT 0,
    FOREIGN KEY (department_id) REFERENCES departments(department_id) ON DELETE SET DEFAULT
);
```
- Explanation: If a department is deleted from the departments table, the department_id in the employees table is set to 0 (or another default value).
### 6. ON UPDATE SET DEFAULT
- Purpose: Sets the foreign key column to its default value when the corresponding primary key in the parent table is updated.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER DEFAULT 0,
    FOREIGN KEY (department_id) REFERENCES departments(department_id) ON UPDATE SET DEFAULT
);
```
- Explanation: If the department_id in the departments table is updated, the corresponding department_id in the employees table is set to its default value.
### 7. ON DELETE NO ACTION or RESTRICT
- Purpose: Prevents the deletion of a row in the parent table if there are related rows in the child table. This is the default behavior if no cascading action is specified.
```
CREATE TABLE employees (
    employee_id NUMBER PRIMARY KEY,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    department_id NUMBER,
    FOREIGN KEY (department_id) REFERENCES departments(department_id) ON DELETE NO ACTION
);
```
- Explanation: If you attempt to delete a department that is referenced by any employees, the deletion will fail.




  





