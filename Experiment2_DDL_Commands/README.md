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
--Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

```sql
create table item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER,
icom_id TEXT(4),
FOREIGN KEY (icom_id) REFERENCES company(com_id)
ON UPDATE CASCADE 
ON DELETE CASCADE
);
```

**Output:**

<img width="1132" height="329" alt="image" src="https://github.com/user-attachments/assets/4b9ec616-2744-4663-bd4c-a41aa4d8967d" />


**Question 2**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```sql
create table Invoices(
InvoiceID integer primary key,
InvoiceDate date,
DueDate date check(DueDate>InvoiceDate),
Amount real check(Amount>0)
);
```

**Output:**

<img width="1151" height="266" alt="image" src="https://github.com/user-attachments/assets/0b088726-aa58-4c3c-8a04-2372adcfcda2" />


**Question 3**
---
Insert the following employees into the Employee table:

EmployeeID  Name        Position    Department  Salary
----------  ----------  ----------  ----------  ----------
2           John Smith  Developer   IT          75000
3           Anna Bell   Designer    Marketing   68000

```sql
INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary)VALUES (2,'John Smith','Developer','IT',75000),(3,'Anna Bell','Designer','Marketing',68000)
```

**Output:**

<img width="1191" height="393" alt="image" src="https://github.com/user-attachments/assets/1ca8bbe3-839b-4745-ae9b-0ee42de00c5f" />

**Question 4** 
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
create table jobs(
job_id integer primary key,
job_title text default '',
min_salary integer default 8000,
max_salary integer default null
);
```

**Output:**

<img width="1144" height="324" alt="image" src="https://github.com/user-attachments/assets/f5270212-b505-4b67-ab2c-eb56bfd29047" />


**Question 5**
---
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT

```sql
create table Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**

<img width="1161" height="364" alt="image" src="https://github.com/user-attachments/assets/a39292c6-b5de-47ed-bee5-846f0c194f1e" />


**Question 6**
---
Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78

```sql
insert into Student_details(RollNO,Name,Gender,Subject,MARKS) values(202,'Ella King','F','Chemistry',87);
insert into Student_details values(203,'James Bond','M','Literature',78);
```

**Output:**

<img width="1154" height="257" alt="image" src="https://github.com/user-attachments/assets/349ebd42-fe5b-4726-905a-b16f9a5b8513" />


**Question 7**
---
Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0

```sql
INSERT INTO Student_details
SELECT * FROM Archived_students
```

**Output:**

<img width="1170" height="276" alt="image" src="https://github.com/user-attachments/assets/b53cd642-7474-4edb-9101-af1c2aee676c" />


**Question 8**
---
Write a SQL query to modify the Student_details table by adding a new column Email of type VARCHAR(50) and updating the column MARKS to have a default value of 0.

```sql
alter table Student_details 
add column Email VARCHAR(50);
alter table Student_details
add column MARKS integer default 0;
```

**Output:**

<img width="1153" height="233" alt="image" src="https://github.com/user-attachments/assets/8b82343f-b526-4b3b-aba2-f54ac8ec348b" />


**Question 9**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```sql
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT not null,
rate INTEGER not null,
icom_id text check(LENGTH(icom_id)==4),
FOREIGN KEY (icom_id) REFERENCES company(com_id)
ON UPDATE SET NULL
ON DELETE SET NULL
);
```

**Output:**

<img width="1142" height="335" alt="image" src="https://github.com/user-attachments/assets/ffb1b7f4-e1ad-41d0-b264-4c55427c96a7" />


**Question 10**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

```sql
INSERT INTO Products(ProductID, Name, Category, Price, Stock) Values(104,'Tablet','Electronics',100,50);
```

**Output:**

<img width="1170" height="266" alt="image" src="https://github.com/user-attachments/assets/34dbbdb6-b998-493e-b24a-c7afce3aaf43" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
