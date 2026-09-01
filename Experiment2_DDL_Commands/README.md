# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```sql
CREATE TABLE Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
DueDate DATE,
Amount REAL,
CHECK (DueDate > InvoiceDate),
CHECK (Amount > 0)
);
```

**Output:**

<img width="1231" height="361" alt="image" src="https://github.com/user-attachments/assets/7a51f5d1-3683-4b26-a927-57d660438726" />


**Question 2**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```sql
CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);
```

**Output:**
<img width="1308" height="325" alt="image" src="https://github.com/user-attachments/assets/3fcd11ef-9e1b-4c61-92e7-c3e3c237f568" />



**Question 3**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
CREATE TABLE Department(
DepartmentID INTEGER PRIMARY KEY,
DepartmentName TEXT UNIQUE NOT NULL,
Location TEXT
)
```

**Output:**

<img width="1903" height="277" alt="image" src="https://github.com/user-attachments/assets/a29c6453-87a8-4849-a3b9-b28d01484a25" />


**Question 4**
---
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER

```sql
CREATE TABLE Orders(
OrderID INTEGER,
OrderDate TEXT,
CustomerID INTEGER
)
```

**Output:**

<img width="1326" height="377" alt="image" src="https://github.com/user-attachments/assets/c651f398-e83a-4bc9-a0cb-e70bc060d907" />


**Question 5**
---
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo                Name                    Gender      
----------            ------------            ----------  
204                   Samuel Black            M          

Note: The Subject and MARKS columns will use their default values.

```sql
INSERT INTO Student_details(RollNo,Name,Gender)
VALUES(204,'Samuel Black','M')
```

**Output:**

<img width="1097" height="327" alt="image" src="https://github.com/user-attachments/assets/3c628a8c-1019-49e5-a5f2-ac4ab9ee0a1d" />


**Question 6**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
INSERT INTO Customers(CustomerID,Name,Address,Email)
SELECT CustomerID,Name,Address,Email
FROM Old_customers
```

**Output:**

<img width="1638" height="342" alt="image" src="https://github.com/user-attachments/assets/1a346641-b17d-48a9-826a-112b2b8e4213" />


**Question 7**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

```sql
INSERT INTO Employee(EmployeeID,Name,Department,Salary)
SELECT EmployeeID,Name,Department,Salary 
FROM Former_employees
```

**Output:**

<img width="1302" height="355" alt="image" src="https://github.com/user-attachments/assets/8d4de3db-4a26-4661-b125-d72d7f44db2b" />


**Question 8**
---
Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0

```sql
ALTER TABLE Student_details
ADD COLUMN Country TEXT
```

**Output:**

<img width="1227" height="288" alt="image" src="https://github.com/user-attachments/assets/777a8db5-0eae-42b5-ba7b-90db4a4b140a" />


**Question 9**
---
Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0

```sql
ALTER TABLE Student_details
ADD COLUMN mobilenumber number
```

**Output:**

<img width="1232" height="283" alt="image" src="https://github.com/user-attachments/assets/2133b7b8-ad7a-41ca-bb53-58d6456bf079" />


**Question 10**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

```sql
CREATE TABLE Employees(
EmployeeID INTEGER PRIMARY KEY,
FirstName TEXT NOT NULL,
LastName TEXT NOT NULL,
Email TEXT UNIQUE,
Salary REAL CHECK(Salary>0),
DepartmentID INTEGER,
FOREIGN KEY(DepartmentID)REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="1337" height="348" alt="image" src="https://github.com/user-attachments/assets/54525d94-2537-474d-937a-343d3e70578a" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
