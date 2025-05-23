# 📊 SQL & NoSQL Database Design and Implementation

**Course:** ICT702 – Introduction to the Relational Database  
**Role:** Group Member – Database Developer & Analyst  
**Technologies Used:** SQL Server, MongoDB (Studio 3T), Power BI, Microsoft Word, Microsoft PowerPoint

---

## 📌 Project Overview

This project explored the design, implementation, and querying of both **relational (SQL)** and **non-relational (NoSQL)** databases through a practical assignment. It simulated real-world scenarios where structured and semi-structured data needed to be efficiently managed and analyzed.

The project was divided into four key sections:

---

## 🧩 Section A – SQL Implementation

- Created a SQL Server database `ICT702_GroupNo_01` using DDL statements.
- Defined and built relational tables: `JOB`, `EMPLOYEE`, `PROJECT`, and `ASSIGNMENT`, applying primary keys, foreign keys, and `NOT NULL` constraints.
- Inserted mock data into each table using DML commands, simulating real business data for HR and project tracking.

## 🛠️ Section A: Basic SQL Implementation

This section involved setting up the foundational relational database structure using **SQL Server**. The implementation includes creating a new database, defining tables with appropriate constraints, and populating them with sample data to simulate a real-world scenario.

---

### 🔧 a. Create Database

```sql
CREATE DATABASE ICT702_GroupNo_01;
GO
DROP TABLE IF EXISTS JOB;
GO
CREATE TABLE JOB (
    Job_Code INT PRIMARY KEY,
    Description VARCHAR(255) NOT NULL,
    Hour DECIMAL(5, 2) NOT NULL,
    Job_Update DATE NOT NULL
);
GO

CREATE TABLE EMPLOYEE (
    Emp_Num INT PRIMARY KEY,
    LName VARCHAR(50) NOT NULL,
    FName VARCHAR(50) NOT NULL,
    HireDate DATE NOT NULL,
    Job_Code INT,
    Emp_Years DECIMAL(5,2) NOT NULL,
    FOREIGN KEY (Job_Code) REFERENCES JOB(Job_Code)
);

CREATE TABLE PROJECT (
    Proj_Num INT PRIMARY KEY,
    Proj_Name VARCHAR(255) NOT NULL,
    Value DECIMAL(18,2) NOT NULL,
    Balance DECIMAL(18,2) NOT NULL,
    Emp_Num INT,
    FOREIGN KEY (Emp_Num) REFERENCES EMPLOYEE(Emp_Num)
);

CREATE TABLE ASSIGNMENT (
    Assi_Num INT PRIMARY KEY,
    Date DATE NOT NULL,
    Proj_Num INT,
    Emp_Num INT,
    Hours DECIMAL(5,2) NOT NULL,
    Charge DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (Proj_Num) REFERENCES PROJECT(Proj_Num),
    FOREIGN KEY (Emp_Num) REFERENCES EMPLOYEE(Emp_Num)
);
-- c. Insert data into JOB table
INSERT INTO JOB (Job_Code, Description, Hour, Job_Update)
VALUES
(500, 'Programmer', 35.75, '2024-11-20'),
(501, 'System Analyst', 96.75, '2024-11-20'),
(502, 'Database Designer', 120.00, '2023-11-22'),
(503, 'Electronic Engineer', 84.5, '2022-11-21'),
(504, 'Mechanical Engineer', 67.9, '2023-11-21'),
(505, 'Civil Engineer', 56.80, '2023-11-20'),
(506, 'Application Designer', 51.25, '2024-11-24'),
(507, 'Data Scientist', 91.5, '2024-02-10');

-- Insert data into EMPLOYEE table
INSERT INTO EMPLOYEE (Emp_Num, LName, FName, HireDate, Job_Code, Emp_Years)
VALUES
(101, 'Jawad', 'Khan', '2025-05-01', 502, 0.5),
(102, 'Rifa', 'Toma', '2025-01-01', 500, 0.5),
(103, 'Shahida', 'Shotto', '2024-12-25', 501, 1),
(104, 'Sana', 'Azim', '2023-01-01', 502, 2),
(105, 'Samim', 'Shaikh', '2019-11-10', 502, 5),
(106, 'LO', 'Anjoj', '2020-01-29', 505, 4),
(107, 'Macario', 'Maria', '2021-01-25', 506, 1),
(108, 'Mahrajan', 'Rajan', '2022-11-20', 501, 2),
(109, 'Johns', 'Alex', '2000-11-08', 504, 12),
(110, 'Johnson', 'Julia', '2005-10-09', 501, 17),
(111, 'Fenny', 'Fenny', '2000-01-01', 507, 3);

-- Insert data into PROJECT table
INSERT INTO PROJECT (Proj_Num, Proj_Name, Value, Balance, Emp_Num)
VALUES
(15, 'Evergreen', 143500.00, 1003550.00, 103),
(18, 'Amber wave', 3500500.00, 2110346.00, 108),
(22, 'Rolling Tide', 805000.00, 500345.20, 102),
(25, 'Solar Installation', 2555000.00, 23809850.00, 109);

-- Insert data into ASSIGNMENT table
INSERT INTO ASSIGNMENT (Assi_Num, Date, Proj_Num, Emp_Num, Hours, Charge)
VALUES
(1001, '2025-04-02', 18, 109, 5.0, 205.00),
(1002, '2025-03-03', 22, 110, 5.1, 140.10),
(1003, '2025-04-22', 18, 110, 2.0, 69.10),
(1004, '2022-10-10', 25, 107, 5.9, 75.50),
(1005, '2022-12-11', 22, 104, 6.5, 65.50),
(1006, '2023-04-01', 15, 101, 10, 80.00),
(1007, '2023-03-05', 22, 102, 9, 60.00),
(1008, '2023-01-01', 18, 101, 14, 66.50),
(1009, '2022-05-10', 15, 104, 8.5, 55.25),
(1010, '2023-05-01', 25, 107, 12, 415.25);```

---

## ⚙️ Section B – Advanced SQL Operations

- Created a derived table `EMPLOYEE1` (a subset of `EMPLOYEE`) and duplicated it to `EMPLOYEE2`.
- Added new fields to `EMPLOYEE2` (`PCT`, `ProjNum`) and performed conditional `UPDATE` operations (e.g., modifying bonus percentages and job roles).
- Deleted dependent records (e.g., “John Alex”) while maintaining referential integrity.
- Executed subqueries, joins, and aggregation to analyze project allocations, employee roles, and bonus distribution.
- Created a **virtual table `EmpVirtual`** to isolate employees not assigned to any project.

## 🔍 Section B: Advanced SQL Queries

```sql
-- d. Create EMPLOYEE1 as subset of EMPLOYEE
CREATE TABLE EMPLOYEE1 (
    Emp_Num INT PRIMARY KEY,
    LName VARCHAR(15) NOT NULL,
    FName VARCHAR(15) NOT NULL,
    HireDate DATE NOT NULL,
    Job_Code INT,
    FOREIGN KEY (Job_Code) REFERENCES JOB(Job_Code)
);

-- e. Insert group member data into EMPLOYEE1 manually
INSERT INTO EMPLOYEE1 (Emp_Num, LName, FName, HireDate, Job_Code)
VALUES 
(101, 'AL', 'Hasib', '2025-04-08', 502),
(102, 'Syed Massir', 'Husain', '2025-01-05', 501),
(103, 'DAHAL', 'Niraj', '2022-12-13', 500);

-- f. Insert remaining records from EMPLOYEE into EMPLOYEE1 using subquery
INSERT INTO EMPLOYEE1 (Emp_Num, LName, FName, HireDate, Job_Code)
SELECT Emp_Num, LName, FName, HireDate, Job_Code
FROM EMPLOYEE
WHERE Emp_Num NOT IN (101, 102, 103);

-- g. Create EMPLOYEE2 by copying EMPLOYEE1 and add new columns
SELECT * INTO EMPLOYEE2 FROM EMPLOYEE1;
ALTER TABLE EMPLOYEE2
ADD PCT NUMERIC(5,2), 
    ProjNum INT;

-- Insert a new record into EMPLOYEE2
BEGIN TRANSACTION;
INSERT INTO EMPLOYEE2 (Emp_Num, LName, FName, HireDate, Job_Code, PCT, ProjNum)
VALUES (101, 'AL', 'Hasib', '2025-04-08', 502, 3.5, 18);
COMMIT;

-- h. Update Job_Code for Emp_Num 107
UPDATE EMPLOYEE
SET Job_Code = 507
WHERE Emp_Num = 107;

-- i. Delete EMPLOYEE record with foreign key handling
UPDATE ASSIGNMENT
SET Emp_Num = NULL 
WHERE Emp_Num = 109;

DELETE FROM ASSIGNMENT WHERE Emp_Num = 109;
DELETE FROM PROJECT WHERE Emp_Num = 109;
DELETE FROM EMPLOYEE WHERE Emp_Num = 109 AND LName = 'Johns' AND FName = 'Alex';

-- j. EMPLOYEE2 already exists, so select data
SELECT * FROM EMPLOYEE2;

-- l. Set PCT to 3.5 for Emp_Num 105
UPDATE EMPLOYEE2
SET PCT = 3.5
WHERE Emp_Num = 105;

-- m. Set PCT = 7.5 for selected Emp_Nums
UPDATE EMPLOYEE2
SET PCT = 7.5
WHERE Emp_Num IN (101, 103, 104);

-- n. Set default PCT = 15 where NULL
UPDATE EMPLOYEE2
SET PCT = 15
WHERE PCT IS NULL;

-- o. Increment PCT by 0.75 for Fenny Fenny
UPDATE EMPLOYEE2
SET PCT = PCT + 0.75
WHERE LName = 'Fenny' AND FName = 'Fenny';

-- p. Display employees not managing any project
SELECT E.Emp_Num, E.FName, E.LName, P.Proj_Num, P.Proj_Name
FROM EMPLOYEE E
LEFT JOIN PROJECT P ON E.Emp_Num = P.Emp_Num
WHERE P.Proj_Num IS NULL;

-- q. Display employees not assigned to any project using subquery
SELECT Emp_Num, FName, LName
FROM EMPLOYEE
WHERE Emp_Num NOT IN (SELECT Emp_Num FROM PROJECT);

-- r. Calculate total balance across all projects
SELECT SUM(Balance) AS Total_Balance
FROM PROJECT;

-- s. Display employees with same Job_Code as Emp_Num = 101
SELECT FName, LName
FROM EMPLOYEE
WHERE Job_Code = (SELECT Job_Code FROM EMPLOYEE WHERE Emp_Num = 101)
ORDER BY FName ASC;

-- t. Create virtual table of employees not in any assignment
SELECT Emp_Num, LName, FName, Job_Code
INTO EmpVirtual
FROM EMPLOYEE
WHERE Emp_Num NOT IN (SELECT Emp_Num FROM ASSIGNMENT);

-- u. Show contents of EmpVirtual table
SELECT * FROM EmpVirtual;```

---

## 📐 Section C – Entity Relationship Diagram (ERD)

- Designed an ERD to represent table relationships:
  - `EMPLOYEE` linked to `JOB` via `Job_Code`
  - `EMPLOYEE` linked to `PROJECT` via `Emp_Num`
  - `ASSIGNMENT` as a many-to-many bridge between `EMPLOYEE` and `PROJECT`

<img width="446" alt="image" src="https://github.com/user-attachments/assets/0ea8e8e5-0329-48ed-8c37-4291022fc4cb" />

The ERD illustrated the logical schema and helped maintain referential integrity throughout the database.

---

## 🧾 Section D – NoSQL Implementation (MongoDB)

- Created a MongoDB database `Assi2Group1` and collection `Assignment`.
- Inserted semi-structured documents with fields like `Emp_Name`, `Proj_Num`, `Hours`, and `Charge`.
- Ran filter queries using MongoDB syntax:
  - Display all records
  - Query by employee name (e.g., `"Julia"`)
  - Exclude records by employee number (e.g., `Emp_Num != 110`)

## 🍃 Section D: NoSQL Implementation (MongoDB)

```javascript
// a. Create the database named 'Assi2Group1'
use Assi2Group1;

// b. Create a new collection called 'Assignment' if it doesn't already exist
db.createCollection("Assignment");

// c. Insert multiple documents into the 'Assignment' collection
db.Assignment.insertMany([
  {
    Emp_Name: "Al Hassib",
    Date: ISODate("2018-03-22T00:00:00Z"),
    Proj_Num: 20,
    Emp_Num: 109,
    Hours: 3.5,
    Charge: 290.50
  },
  {
    Emp_Name: "Shahida",
    Date: ISODate("2019-03-22T00:00:00Z"),
    Proj_Num: 22,
    Emp_Num: 110,
    Hours: 4.2,
    Charge: 140.00
  },
  {
    Emp_Name: "Julia",
    Date: ISODate("2019-04-22T00:00:00Z"),
    Proj_Num: 18,
    Emp_Num: 110,
    Hours: 2.0,
    Charge: 72.50
  },
  {
    Emp_Name: "Sarah",
    Date: ISODate("2022-10-10T00:00:00Z"),
    Proj_Num: 25,
    Emp_Num: 107,
    Hours: 5.9,
    Charge: 79.00
  },
  {
    Emp_Name: "Ali",
    Date: ISODate("2022-12-11T00:00:00Z"),
    Proj_Num: 22,
    Emp_Num: 104,
    Hours: 6.5,
    Charge: 65.50
  }
]);

// d. Retrieve and display all documents from the 'Assignment' collection
db.Assignment.find({}).pretty();

// e. Find and show all documents where the employee's name is 'Julia'
db.Assignment.find(
  { Emp_Name: "Julia" }
).pretty();

// f. Find and show all documents where Emp_Num is NOT equal to 110
db.Assignment.find(
  { Emp_Num: { $ne: 110 } }
).pretty();```


MongoDB demonstrated flexibility in handling schema-less data and provided an excellent contrast to the structured SQL setup.

---

## 🎯 Key Takeaways

- Gained hands-on experience in **SQL schema design**, **DML/DDL**, and advanced querying techniques.
- Learned to manage data dependencies using **foreign keys**, `JOIN`s, and cascading deletions.
- Practiced document-based storage and retrieval in **MongoDB** using **NoSQL** principles.
- Understood how SQL and NoSQL can be integrated for hybrid database systems.
- Developed skills in **data modeling**, **query optimization**, and **reporting**.

---

## 🏁 Conclusion

This project served as a full-stack learning experience in data management. It highlighted the differences and complementarities between SQL and NoSQL, reinforced best practices in schema design, and enhanced our ability to query and manipulate data in both structured and semi-structured environments. The assignment not only expanded our technical capabilities but also our documentation and problem-solving skills, essential for modern data-driven roles.

---

