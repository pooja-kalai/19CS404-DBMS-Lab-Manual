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
Create a table named Shipments with the following constraints: ShipmentID as INTEGER should be the primary key. ShipmentDate as DATE. SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID). OrderID as INTEGER should be a foreign key referencing Orders(OrderID).


```CREATE TABLE Shipments(
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderID INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
    );
```

**Output:**
<img width="1241" height="323" alt="image" src="https://github.com/user-attachments/assets/aa1ea790-a9db-4e41-85e7-522d7c75c07d" />


**Question 2**
---
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

```
INSERT INTO Student_details (RollNo,Name,Gender,Subject,MARKS) VALUES (201,'David Lee','M','Physics',92)
```

**Output:**
<img width="1243" height="340" alt="image" src="https://github.com/user-attachments/assets/73580108-b990-4642-af25-9a9b9838e9d9" />


**Question 3**
---
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

```
ALTER TABLE employees ADD COLUMN salary INTEGER CHECK (salary>0)
```

**Output:**

<img width="1233" height="368" alt="image" src="https://github.com/user-attachments/assets/8f2d8a18-7fcc-49be-8660-161c5eaee7ad" />


**Question 4**
---
Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types: designation as VARCHAR(50) net_salary as NUMBER dob as DATE

```
ALTER TABLE Companies ADD COLUMN designation varchar(50);
ALTER TABLE Companies ADD COLUMN net_salary number;
ALTER TABLE Companies ADD COLUMN dob date;
```

**Output:**
<img width="1232" height="513" alt="image" src="https://github.com/user-attachments/assets/41636792-edca-41c3-ac0f-19ea745c1ae3" />



**Question 5**
---
Create a table named Orders with the following constraints: OrderID as INTEGER should be the primary key. OrderDate as DATE should be not NULL. CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```
CREATE TABLE Orders(
    OrderID INTEGER PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);


```

**Output:**

<img width="1228" height="376" alt="image" src="https://github.com/user-attachments/assets/0cb37162-b19d-48d2-954e-9455579c213e" />


**Question 6**
---
Create a table named Attendance with the following constraints: AttendanceID as INTEGER should be the primary key. EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID). AttendanceDate as DATE. Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```
CREATE TABLE Attendance(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK (Status IN ('Present','Absent','Leave')),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
    );
```

**Output:**
<img width="1231" height="377" alt="image" src="https://github.com/user-attachments/assets/0c714802-a38a-4120-a8eb-d78d4b80080b" />


**Question 7**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

```
INSERT INTO Employee SELECT * FROM Former_employees;
```

**Output:**
<img width="1233" height="365" alt="image" src="https://github.com/user-attachments/assets/44bf9afe-8509-4d7d-a06e-295a09494ce9" />



**Question 8**
---
Create a table named Products with the following constraints:

ProductID should be the primary key. ProductName should be NOT NULL. Price is of real datatype and should be greater than 0. Stock is of integer datatype and should be greater than or equal to 0.

```
CREATE TABLE Products(
    ProductID PRIMARY KEY,
    ProductName NOT NULL,
    Price REAL CHECK (Price > 0),
    Stock INTEGER CHECK(Stock>=0)
);
```

**Output:**

<img width="1247" height="366" alt="image" src="https://github.com/user-attachments/assets/3f95cb13-4be0-48a0-928c-9be0e213dec5" />


**Question 9**
---
Insert the following employees into the Employee table:

EmployeeID Name Position Department Salary

```
INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary) VALUES (2,'John Smith','Developer','IT',75000);
INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary) VALUES (3,'Anna Bell','Designer','Marketing',68000);
```

**Output:**
<img width="1240" height="447" alt="image" src="https://github.com/user-attachments/assets/8116f0e7-3e96-46c2-9fb2-14b5eca72041" />


**Question 10**
---
Create a table named Departments with the following columns:

DepartmentID as INTEGER DepartmentName as TEXT

```
CREATE TABLE Departments(
    DepartmentID INTEGER,
    DepartmentName TEXT


);
```

**Output:**
<img width="1238" height="447" alt="image" src="https://github.com/user-attachments/assets/07eecb9e-49d1-4ac6-81f0-b69d61094460" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
