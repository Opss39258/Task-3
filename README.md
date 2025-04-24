# SQL Operations on Employees Table

This README documents various SQL operations executed on the `Employees` table in a MySQL database using MySQL Workbench. The operations include `SELECT`, filtering, ordering, grouping, subqueries, aggregate functions, views, and optimization using indexes.

---

## Table Structure

### Employees
| Column     | Type           |
|------------|----------------|
| EmpID      | INT (Primary Key) |
| Name       | VARCHAR(50)    |
| Department | VARCHAR(30)    |
| Salary     | DECIMAL(10,2)  |

---

## a. SELECT, WHERE, ORDER BY, GROUP BY

```sql
-- Select all employees
SELECT * FROM Employees;

-- Select employees with salary greater than 50,000
SELECT * FROM Employees
WHERE Salary > 50000;

-- Order employees by salary descending
SELECT * FROM Employees
ORDER BY Salary DESC;

-- Group by department and count employees in each
SELECT Department, COUNT(*) AS Total_Employees
FROM Employees
GROUP BY Department;
```

---

## b. JOINS (Simulated using self-join for illustration)

Since there's no separate Departments table, here’s a simulated example using self-join to demonstrate JOINs:

```sql
-- INNER JOIN (self-join example)
SELECT e1.Name AS Employee1, e2.Name AS Employee2, e1.Department
FROM Employees e1
INNER JOIN Employees e2 ON e1.Department = e2.Department
WHERE e1.EmpID < e2.EmpID;

-- LEFT JOIN simulation: Select all employees and compare with others in same department
SELECT e1.Name AS Employee, e2.Name AS Colleague, e1.Department
FROM Employees e1
LEFT JOIN Employees e2 ON e1.Department = e2.Department AND e1.EmpID <> e2.EmpID;

-- RIGHT JOIN is not directly applicable without a second table
```

---

## c. Subqueries

```sql
-- Employees who earn more than the average salary
SELECT * FROM Employees
WHERE Salary > (SELECT AVG(Salary) FROM Employees);

-- Department of the highest paid employee
SELECT Department FROM Employees
WHERE Salary = (SELECT MAX(Salary) FROM Employees);
```

---

## d. Aggregate Functions

```sql
-- Total salary paid
SELECT SUM(Salary) AS Total_Salary FROM Employees;

-- Average salary per department
SELECT Department, AVG(Salary) AS Avg_Salary
FROM Employees
GROUP BY Department;
```

---

## e. Create Views for Analysis

```sql
-- View showing employees with high salaries
CREATE VIEW HighEarners AS
SELECT * FROM Employees
WHERE Salary > 55000;

-- Query the view
SELECT * FROM HighEarners;
```

---

## f. Optimize Queries with Indexes

```sql
-- Create index on Salary for faster filtering
CREATE INDEX idx_salary ON Employees(Salary);

-- Create index on Department for faster grouping
CREATE INDEX idx_department ON Employees(Department);
```

---

## Sample Data

| EmpID | Name            | Department | Salary   |
|-------|-----------------|------------|----------|
| 1     | John Doe        | HR         | 50000.00 |
| 2     | Jane Smith      | IT         | 60000.00 |
| 3     | Alice Johnson   | Finance    | 55000.00 |
| 4     | Bob Brown       | HR         | 45000.00 |
| 5     | Charlie White   | IT         | 65000.00 |
