# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
SELECT* FROM CUSTOMERS WHERE SALARY<2500;
```

**Output:**
<img width="872" height="545" alt="image" src="https://github.com/user-attachments/assets/408a2505-8f46-48cd-8b03-bb5cf3933b5a" />



**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
SELECT* FROM CUSTOMERS WHERE SALARY=1500;
```

**Output:**
<img width="853" height="419" alt="image" src="https://github.com/user-attachments/assets/554b3886-5470-4344-a3a9-2d7867c0349d" />



**Question 3**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT name,city FROM customer WHERE city IN(SELECT city FROM customer WHERE id IN(3,7));

```

**Output:**

<img width="830" height="531" alt="image" src="https://github.com/user-attachments/assets/8d1b67ee-68fc-43b2-a891-0a136a0e5ed6" />


**Question 4**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)



For example:

```sql
SELECT* FROM Medications WHERE dosage IN (SELECT MAX(dosage) FROM Medications);
```

**Output:**

<img width="907" height="483" alt="image" src="https://github.com/user-attachments/assets/425ba331-f951-4764-9ee5-fe6162c1a809" />


**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
SELECT* FROM CUSTOMERS WHERE ID IN(SELECT ID FROM CUSTOMERS WHERE ADDRESS="Delhi" AND age<30);
```

**Output:**

<img width="821" height="455" alt="image" src="https://github.com/user-attachments/assets/eda4eab2-fa5d-47cd-a3a7-f72fdae8ac8f" />


**Question 6**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



```sql
SELECT student_name, grade FROM GRADES t1 WHERE grade=(SELECT MAX(grade) FROM GRADES t2 WHERE t2.subject=t1.subject);
```

**Output:**

<img width="805" height="505" alt="image" src="https://github.com/user-attachments/assets/fd5d4693-a546-495d-8461-4e3607b5aa1f" />


**Question 7**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



```sql
SELECT student_id,student_name,subject, grade FROM GRADES t1 WHERE grade=(SELECT MAX(grade) FROM GRADES t2 WHERE t2.subject=t1.subject);
```

**Output:**

<img width="889" height="519" alt="image" src="https://github.com/user-attachments/assets/4b44cd5a-aec9-4617-a452-ceb90048049c" />


**Question 8**
---
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)



```sql
SELECT* FROM Departments WHERE LENGTH(department_name)>(SELECT AVG(LENGTH(department_name)) FROM Departments);
```

**Output:**

<img width="707" height="457" alt="image" src="https://github.com/user-attachments/assets/1577b903-8480-497f-b4f3-5e11cfe683ca" />


**Question 9**
---
From the following tables write a SQL query to find all orders generated by London-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM orders o
JOIN salesman s ON o.salesman_id = s.salesman_id
WHERE s.city = 'London';
```

**Output:**

<img width="882" height="487" alt="image" src="https://github.com/user-attachments/assets/d168984f-8765-43c5-8277-c1ba441156e3" />


**Question 10**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
SELECT * FROM CUSTOMERS WHERE AGE < 30;
```

**Output:**

<img width="844" height="628" alt="image" src="https://github.com/user-attachments/assets/7128efce-0115-4e79-b09b-e196907384a4" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
