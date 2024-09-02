
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



```
SELECT column1, column2, column3
FROM table_name;
```
```
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







