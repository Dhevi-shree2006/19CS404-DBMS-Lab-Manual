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
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES

```sql
SELECT student_name,grade
FROM GRADES
WHERE(subject,grade) IN (
SELECT subject,MAX(grade)
FROM GRADES
GROUP BY subject
);
```

**Output:**

<img width="817" height="452" alt="image" src="https://github.com/user-attachments/assets/d04cfe1d-1f9b-4291-b40c-882b3d976b2e" />


**Question 2**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Medications Table

```sql
SELECT medication_id,medication_name,dosage
FROM Medications
WHERE dosage = (SELECT MIN(dosage) 
                FROM Medications);
```

**Output:**

<img width="1037" height="428" alt="image" src="https://github.com/user-attachments/assets/081368d4-76cb-4afe-8da5-12fea73b2f38" />


**Question 3**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT *
FROM customer
WHERE city!=(
    SELECT city
    FROM customer
    ORDER BY id DESC
    LIMIT 1
);
```

**Output:**

<img width="1251" height="511" alt="image" src="https://github.com/user-attachments/assets/07925dbb-f74f-4e85-b7b5-22e2a0cefd54" />


**Question 4**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table

```sql
SELECT *
FROM Employee
WHERE age < (
            SELECT AVG(age)
            FROM Employee
            WHERE income > 1000000
            );
            
```

**Output:**

<img width="1253" height="488" alt="image" src="https://github.com/user-attachments/assets/e6c0f4f6-53fc-4cb4-859a-77c63e8e554c" />


**Question 5**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT name
FROM customer
WHERE phone IN(
            SELECT phone
            FROM customer
            GROUP BY phone
            HAVING COUNT(phone)=1
            );
```

**Output:**

<img width="591" height="530" alt="image" src="https://github.com/user-attachments/assets/5d9df634-fd0b-45a7-9290-1898efd5c277" />


**Question 6**
---
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

```sql
SELECT s.salesman_id,s.name
FROM salesman s
JOIN customer C ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id , s.name
HAVING COUNT(c.customer_id)>1;
```

**Output:**

<img width="667" height="546" alt="image" src="https://github.com/user-attachments/assets/06619662-5451-4b78-a9d3-f69716640a74" />


**Question 7**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

```sql
SELECT *
FROM customer
WHERE customer_id=(
                SELECT salesman_id
                FROM salesman
                WHERE name='Mc Lyon'
                )-2001;
```

**Output:**

<img width="1232" height="423" alt="image" src="https://github.com/user-attachments/assets/e6d092ad-e21f-4b86-96c8-66be109636f4" />


**Question 8**
---
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

```sql
SELECT *
FROM Orders
WHERE salesman_id=(
                SELECT salesman_id
                FROM Salesman
                WHERE name='Paul Adam'
                );
```

**Output:**

<img width="1231" height="496" alt="image" src="https://github.com/user-attachments/assets/d5393e60-c6ec-45cc-9408-b1ae53f7485d" />


**Question 9**
---
From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

```sql
SELECT commission
FROM salesman
WHERE salesman_id IN (
                    SELECT salesman_id
                    FROM customer
                    WHERE city='Paris'
                    );
```

**Output:**

<img width="455" height="410" alt="image" src="https://github.com/user-attachments/assets/94433752-3b4d-4364-93cd-1e5faaa2866f" />


**Question 10**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY>4500;
```

**Output:**

<img width="1222" height="518" alt="image" src="https://github.com/user-attachments/assets/697fbd6f-7e6a-497c-b220-f9c702e517d8" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
