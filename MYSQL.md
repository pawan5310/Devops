## **1. Introduction to SQL & DBMS**

- **What is SQL?**
  - SQL stands for **Structured Query Language**.
  - It is a standardized language used to **store, manipulate, and retrieve data** in databases.
  - SQL works with various DBMS (Database Management Systems) like MySQL, Oracle, SQL Server, and MongoDB.

- **What is MySQL?**
  - MySQL is a popular open-source DBMS that uses SQL.

***

## **2. Installation and Setup**

- Install **XAMPP** (for running MySQL server) and **MySQL Workbench** (GUI client).
- Start Apache and MySQL from XAMPP, then use MySQL Workbench or CLI for running queries.

***

## **3. Basic Database Concepts**

- **Database**: Organized storage area for related data (like a computerized register).
- **Table**: Structure to store data in rows and columns.
- **Field/Column**: Individual attribute (e.g., Name, Age).
- **Record/Row**: One complete set of data in a table.

***

## **4. Creating/Selecting a Database**

```sql
-- Create a database named 'company'
CREATE DATABASE company;

-- Select database for use
USE company;

-- Show all databases
SHOW DATABASES;

-- Drop a database
DROP DATABASE company;
```

***

## **5. Creating a Table**

```sql
CREATE TABLE employee_info (
    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,  -- Auto incrementing primary key
    emp_name VARCHAR(30) NOT NULL,
    address VARCHAR(255) NOT NULL,
    city VARCHAR(20) NOT NULL,
    age INT NOT NULL,
    doj DATE NOT NULL,         -- Date of joining
    designation VARCHAR(20) NOT NULL,
    salary DECIMAL(10, 2) NOT NULL,
    mobile VARCHAR(10) NOT NULL
);

-- See structure of table
DESCRIBE employee_info;
```

***

## **6. Insert, View, and Manipulate Data**

### **Insert Data**
```sql
INSERT INTO employee_info 
(emp_name, address, city, age, doj, designation, salary, mobile) 
VALUES
('Kamlesh', 'Ajmer', 'Jaipur', 35, '2008-05-04', 'Programmer', 3000.50, '9810012345'),
('Sunil', 'Jodhpur', 'Udaipur', 41, '2012-11-20', 'Manager', 6000.00, '9820012345');
```

### **View Data**
```sql
-- See all data
SELECT * FROM employee_info;

-- See selected columns only
SELECT emp_name, mobile FROM employee_info;
```

***

## **7. Filtering Data**

### **WHERE Clause**
```sql
SELECT * FROM employee_info WHERE designation = 'Programmer';
```

### **AND, OR Operators**
```sql
SELECT * FROM employee_info WHERE designation = 'Programmer' AND city = 'Jaipur';
SELECT * FROM employee_info WHERE city = 'Jaipur' OR salary = 4200;
```

### **NOT, LIKE, IN, BETWEEN Operators**
```sql
SELECT * FROM employee_info WHERE city NOT LIKE 'Jaipur';
SELECT * FROM employee_info WHERE city IN ('Ajmer', 'Udaipur');
SELECT * FROM employee_info WHERE salary BETWEEN 3000 AND 6000;
```

***

## **8. Updating and Deleting Data**

### **Update Data**
```sql
UPDATE employee_info SET address = 'New Ajmer' WHERE id = 2;
UPDATE employee_info SET salary = 6500 WHERE id = 2;
```

### **Delete Data**
```sql
DELETE FROM employee_info WHERE id = 1;
```

***

## **9. Table Alteration**

### **Add Column**
```sql
ALTER TABLE employee_info ADD email VARCHAR(50);
```
### **Delete Column**
```sql
ALTER TABLE employee_info DROP COLUMN email;
```
### **Change Column**
```sql
ALTER TABLE employee_info MODIFY salary DECIMAL(12,2);
```
### **Drop Table**
```sql
DROP TABLE employee_info;
```

***

## **10. Sorting and Limiting Data**

```sql
SELECT * FROM employee_info ORDER BY salary DESC;  -- Sort Descending
SELECT * FROM employee_info ORDER BY emp_name ASC; -- Sort Ascending
SELECT * FROM employee_info LIMIT 3;               -- Limit to top 3 rows
```

***

## **11. Aggregate Functions**

```sql
SELECT COUNT(*) FROM employee_info;       -- Number of employees
SELECT SUM(salary) FROM employee_info;    -- Total salary
SELECT AVG(salary) FROM employee_info;    -- Average salary
SELECT MIN(salary) FROM employee_info;    -- Minimum salary
SELECT MAX(salary) FROM employee_info;    -- Maximum salary
```

***

## **12. Joins (Combining Data from Multiple Tables)**

#### **Creating Second Table (Department)**
```sql
CREATE TABLE department (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(20)
);

-- Add some departments
INSERT INTO department VALUES (1, 'HR'), (2, 'IT'), (3, 'Accounts');
```

#### **Adding Department ID to Employee Table**
```sql
ALTER TABLE employee_info ADD department_id INT;
ALTER TABLE employee_info ADD FOREIGN KEY (department_id) REFERENCES department(department_id);
```

#### **Inner Join Example**
```sql
SELECT e.emp_name, d.department_name 
FROM employee_info e
INNER JOIN department d ON e.department_id = d.department_id;
```

***

## **13. Constraints**

- **NOT NULL**: Prevents empty values
- **UNIQUE**: No duplicates
- **DEFAULT**: Adds a default value
- **CHECK**: Ensures values meet criteria
- **PRIMARY KEY**: Unique, not null, identifier
- **FOREIGN KEY**: Ensures referential integrity

**Example with Constraints:**
```sql
CREATE TABLE student (
    student_id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    class VARCHAR(10) DEFAULT 'NA',
    age INT CHECK(age >= 3)
);
```

***

## **14. Grouping Data**

```sql
SELECT designation, COUNT(*) AS count FROM employee_info GROUP BY designation;
SELECT city, SUM(salary) FROM employee_info GROUP BY city HAVING SUM(salary)>10000;
```

***

## **15. Backup, Copy, Export**

- Copy data from one table to another:
```sql
CREATE TABLE employee_backup LIKE employee_info;
INSERT INTO employee_backup SELECT * FROM employee_info;
```

- Export/Import via .*csv* or Excel using GUI tools.

***


[VIDEO](https://www.youtube.com/watch?v=7wj7UEdLI6U)
