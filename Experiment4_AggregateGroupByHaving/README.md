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
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

```sql
SELECT SUM(purch_amt) AS TOTAL
FROM orders;
```

**Output:**

![Output1](output.png)

**Question 2**
---
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city

Table: customer

```sql
SELECT AVG(LENGTH(email)) AS avg_email_length_below_30 
FROM customer
WHERE city='Mumbai';
```

**Output:**

![Output2](output.png)

**Question 3**
---
Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

```sql
SELECT COUNT(*) AS COUNT FROM customer;
```

**Output:**

![Output3](output.png)

**Question 4**
---
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table

```sql
SELECT DoctorID , COUNT(AppointmentID)  AS TotalAppointments 
FROM Appointments
GROUP BY DoctorID;
```

**Output:**

![Output4](output.png)

**Question 5**
---
How many patients have expired insurance coverage for each insurance company?

Sample table:Insurance Table

```sql
SELECT InsuranceCompany , COUNT(*) AS TotalExpiredPatients 
FROM Insurance
WHERE date(Substr(ValidityPeriod,15)) < date('now')
GROUP BY InsuranceCompany;
```

**Output:**

![Output5](output.png)

**Question 6**
---
What is the total number of appointments scheduled for each day?

Sample table:Appointments Table

```sql
SELECT DATE(AppointmentDateTime) AS AppointmentDate , COUNT(*) AS TotalAppointments 
FROM Appointments
GROUP BY DATE(AppointmentDateTime)
ORDER BY DATE(AppointmentDateTime);
```

**Output:**

![Output6](output.png)

**Question 7**
---
Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.

Sample table: customer1

```sql
SELECT (age / 5) * 5 AS age_group,MIN(age)
FROM customer1
GROUP BY (age / 5) * 5
HAVING MIN(age) < 25;
```

**Output:**

![Output7](output.png)

**Question 8**
---
Which cities (addresses) in the "customer1" table have an average salary lesser than Rs. 15000

Sample table: customer1

```sql
SELECT address, AVG(salary)
FROM customer1
GROUP BY address
HAVING AVG(salary) < 15000;
```

**Output:**

![Output8](output.png)

**Question 9**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the average income for each age group, and includes only those age groups where the average income falls between 300,000 and 500,000.

Sample table: employee

```sql
SELECT age, AVG(income)
FROM employee
GROUP BY age
HAVING AVG(income) BETWEEN 300000 AND 500000;
```

**Output:**





**Question 10**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products

```sql
SELECT category_id , count(product_name)
FROM products
GROUP BY category_id
HAVING MIN(category_id) < 3;
```

**Output:**





## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
