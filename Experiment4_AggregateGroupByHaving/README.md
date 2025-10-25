# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many patients are there in each city?

Sample table: Patients Table



For example:

Result
Address     TotalPatients
----------  -------------
Berlin      3
Chicago     4
Mexico      3


```sql
SELECT Address, COUNT(*) AS TotalPatients FROM Patients GROUP BY Address;
```

**Output:**
<img width="790" height="410" alt="image" src="https://github.com/user-attachments/assets/aa59d9a7-0819-4a8f-a822-40ec515522cc" />



**Question 2**
---
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table



For example:

Result
PatientID   AvgMedications
----------  --------------
4           5
6           1
7           1
8           3


```sql
select PatientID,COUNT(Medications) AS AvgMedications from MedicalRecords GROUP BY PatientID
```

**Output:**

<img width="818" height="600" alt="image" src="https://github.com/user-attachments/assets/389767eb-28af-47bc-87c8-0ca8e841919b" />


**Question 3**
---
How many medical records does each doctor have?

Sample table:MedicalRecords Table



For example:

Result
DoctorID    TotalRecords
----------  ------------
3           4
5           1
6           1
7           1
8           3


```sql
SELECT DoctorID, COUNT(*) AS TotalRecords FROM MedicalRecords GROUP BY DoctorID;
```

**Output:**

<img width="780" height="612" alt="image" src="https://github.com/user-attachments/assets/889cdd92-d2e9-4c28-82cc-35ac97ad42f3" />


**Question 4**
---
Write a SQL query to find the average length of email addresses (in characters):

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_email_length
----------------
15.0


```sql
select AVG(LENGTH(email)) AS avg_email_length FROM customer;
```

**Output:**

<img width="505" height="321" alt="image" src="https://github.com/user-attachments/assets/2d6992d5-0a2a-4ec4-8e31-c44edc0bd120" />


**Question 5**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
fruit_name  lowest_quantity
----------  ---------------
Watermelon  15


```sql
select name AS fruit_name, inventory AS lowest_quantity FROM fruits ORDER BY inventory ASC LIMIT 1;
```

**Output:**

<img width="704" height="299" alt="image" src="https://github.com/user-attachments/assets/6e49f199-1b92-4e37-ad58-fe1892adcd6e" />


**Question 6**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
5


```sql
select COUNT(*) AS COUNT  FROM employee where age >32;
```

**Output:**

<img width="442" height="298" alt="image" src="https://github.com/user-attachments/assets/1ccfea9e-0cec-48c0-83af-2843529d3a98" />


**Question 7**
---
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MINIMUM
----------
65.26


```sql
select MIN(purch_amt) AS MINIMUM FROM orders;
```

**Output:**

<img width="469" height="309" alt="image" src="https://github.com/user-attachments/assets/91eda1a4-48be-4ae0-9375-3c8092f3c02d" />

**Question 8**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.

Sample table: employee



For example:

Result
age         Income
----------  ----------
32          200000
40          350000
45          450000


```sql
select age, MIN(income) AS Income FROM employee GROUP BY age Having MIN(income) <1000000
```

**Output:**

<img width="623" height="410" alt="image" src="https://github.com/user-attachments/assets/b44fedb0-629c-4d61-888e-4269838afb46" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 400,000.

Sample table: employee



For example:

Result
age         MIN(income)
----------  -----------
32          200000
40          350000


```sql
select age, MIN(income) FROM employee GROUP BY age Having MIN(income) <400000
```

**Output:**

<img width="599" height="364" alt="image" src="https://github.com/user-attachments/assets/8563e1d1-6220-405b-b70e-aadd89c6a230" />


**Question 10**
---
Write the SQL query that accomplishes the selection of number of products for each category from products table which includes only those products where the category ID is greater than 2.

Sample table: products



For example:

Result
category_id  COUNT
-----------  ----------
3            3


```sql
select category_id, COUNT(*) AS COUNT From Products WHERE category_id >2 GROUP BY category_id;
```

**Output:**
<img width="641" height="338" alt="image" src="https://github.com/user-attachments/assets/8ccc2e72-48ea-4380-ae4a-d2869266951b" />





## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
