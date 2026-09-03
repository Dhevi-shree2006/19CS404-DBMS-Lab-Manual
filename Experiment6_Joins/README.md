# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test names 'Blood Test' or 'Blood Pressure' and results not containing the substring 'Normal'.

```sql
SELECT p.*
FROM PATIENTS p
INNER JOIN TEST_RESULTS t ON p.patient_id=t.patient_id
WHERE t.test_name IN ('Blood Test','Blood Pressure') AND t.result NOT LIKE '%NORMAL%';
```

**Output:**

<img width="1288" height="387" alt="image" src="https://github.com/user-attachments/assets/2aebf1f6-549d-40ae-99ba-4467dc5bafe7" />


**Question 2**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.

```sql
SELECT c.cust_name
FROM CUSTOMER c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.purch_amt < 100;
```

**Output:**

<img width="417" height="446" alt="image" src="https://github.com/user-attachments/assets/ef868015-493f-4af7-bb7d-4f1bd24d0856" />


**Question 3**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

```sql
SELECT p.first_name AS patient_name,d.specialization AS Doctor_specialization
FROM PATIENTS p
INNER JOIN DOCTORS d ON p.doctor_id = d.doctor_id
WHERE p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**

<img width="676" height="363" alt="image" src="https://github.com/user-attachments/assets/54db8034-a7bb-46d2-ad12-93a8729c553a" />


**Question 4**
---
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.:

```sql
SELECT p.first_name
FROM PATIENTS p
INNER JOIN SURGERIES s ON P.patient_id=s.patient_id
WHERE s.surgery_date = '2024-01-15';
```

**Output:**

<img width="468" height="408" alt="image" src="https://github.com/user-attachments/assets/d433b4e4-92bf-45ad-9b92-e3e87c71265e" />

**Question 5**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.

```sql
SELECT s.name,c.cust_name,c.city,c.grade,c.salesman_id
FROM Salesman s
LEFT JOIN customer c ON s.salesman_id=c.salesman_id
WHERE c.grade <=100;
```

**Output:**

<img width="1275" height="532" alt="image" src="https://github.com/user-attachments/assets/7357877c-1c34-4867-a756-6bad08c37990" />


**Question 6**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.
```sql
SELECT c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt AS "Order Amount",s.name,s.commission
FROM customer c
LEFT JOIN orders o ON c.customer_id=o.customer_id
LEFT JOIN salesman s ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1278" height="973" alt="image" src="https://github.com/user-attachments/assets/a6f2725e-f734-4ce8-a92d-f8c9e1efc8a4" />


**Question 7**
---
Write the SQL query that achieves the selection of the "nurse_id" from the "nurses" table (aliased as "n") and the "department_name" from the "departments" table, with an inner join on the "department_id" column and conditions filtering for a nurse with the first name 'David' and last name 'Moore'.

```sql
SELECT n.nurse_id,d.department_name
FROM NURSES n
INNER JOIN DEPARTMENTS d ON n.department_id = d.department_id
WHERE n.first_name = 'David' AND n.last_name = 'Moore';
```

**Output:**

<img width="780" height="415" alt="image" src="https://github.com/user-attachments/assets/0c2b7b17-8b14-458e-8f47-c070d69094f9" />


**Question 8**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

```sql
SELECT s.name AS salesman_name,c.cust_name AS customer_name
FROM Salesman s
LEFT JOIN customer c ON s.salesman_id=c.salesman_id;
```

**Output:**

<img width="767" height="897" alt="image" src="https://github.com/user-attachments/assets/d908139a-d799-434d-9c97-8209954fdac3" />


**Question 9**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a non-null discharge date.

```sql
SELECT p.first_name AS patient_name,d.first_name AS doctor_name
FROM PATIENTS p
INNER JOIN DOCTORS d ON p.doctor_id = d.doctor_id
WHERE p.discharge_date IS NOT NULL;
```

**Output:**

<img width="813" height="425" alt="image" src="https://github.com/user-attachments/assets/6bd97b81-7cd3-4478-96aa-f2642cfce7a4" />


**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

```sql
SELECT n.*,d.department_name
FROM NURSES n
INNER JOIN DEPARTMENTS d ON n.department_id = d.department_id;
```

**Output:**

<img width="1261" height="583" alt="image" src="https://github.com/user-attachments/assets/5811194f-b251-44b2-987a-a746557e6c0a" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
