# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

Sample table: Customer

```sql
DELETE FROM Customer
WHERE (GRADE = 3 OR AGENT_CODE = 'A008') AND OUTSTANDING_AMT < 5000;
```

**Output:**

<img width="1253" height="461" alt="image" src="https://github.com/user-attachments/assets/e446605d-15d3-4cd3-a7bb-c31fd42f74dd" />


**Question 2**
---
Write a SQL query to calculate the discounted price for products where the discount percentage is greater than 0, and order the results by discounted_price in ascending order. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

| product_id | original_price | discount_percentage |
|------------|----------------|---------------------|
| 101        | 50.00          | 0.10                |
| 102        | 75.00          | 0.00                |
| 103        | 100.00         | 0.20                |

```sql
SELECT product_id,original_price,discount_percentage,(original_price-(original_price * discount_percentage)) AS discounted_price
FROM Products
WHERE discount_percentage > 0
ORDER BY discounted_price ASC;
```

**Output:**

<img width="1230" height="360" alt="image" src="https://github.com/user-attachments/assets/e085c448-bcfc-4378-a295-ca4943fa0adb" />


**Question 3**
---
Write a SQL statement to Change the category to 'Household' where product name contains 'Detergent' in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT           

```sql
UPDATE Products
SET category = 'Household'
WHERE product_name LIKE '%Detergent%';
```

**Output:**

<img width="1293" height="272" alt="image" src="https://github.com/user-attachments/assets/fecb21b0-f9f9-44a0-af06-ff1e098ba0e9" />


**Question 4**
---
Change the supplier name to upper case where contact person contains ' Singh' in suppliers table.

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)

```sql
UPDATE suppliers
SET supplier_name = UPPER(supplier_name) 
WHERE contact_person LIKE '%Singh%';
```

**Output:**

<img width="1497" height="227" alt="image" src="https://github.com/user-attachments/assets/1aae74ca-a69a-4243-85a1-83131f7fccb7" />


**Question 5**
---
Write a query to list all products where the discount amount exceeds $50. The discount amount is calculated as original_price * discount_percentage. Return product_id, original_price, discount_percentage, and discount_amount.

Sample table: Products

product_id | original_price | discount_percentage

-----------------------------------------------------------

"101" "50" "0.1"

"102" "150" "0.15"

"103" "200" "0.2"

"104" "300" "0.25"

```sql
SELECT product_id,original_price, discount_percentage,(original_price * discount_percentage) AS discount_amount
FROM Products
WHERE (original_price * discount_percentage) > 50;
```

**Output:**

<img width="1566" height="340" alt="image" src="https://github.com/user-attachments/assets/44f82749-b82d-4a84-b9bc-a6e3c8d130be" />


**Question 6**
---
Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.


Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id 

```sql
UPDATE employees
SET first_name = 'John'
WHERE department_id = 80 AND commission_pct < 0.35;
```

**Output:**

<img width="1735" height="387" alt="image" src="https://github.com/user-attachments/assets/2cea659a-3b23-4459-8c50-be0f51bf616e" />


**Question 7**
---Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

 
Sample table: Customer 

```sql
DELETE FROM customer
WHERE GRADE < 2;
```

**Output:**

<img width="747" height="590" alt="image" src="https://github.com/user-attachments/assets/59bc30de-939c-4f05-b666-7779f171b12a" />


**Question 8**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3

Sample table: Surgeries


attributes: surgery_id, patient_id, surgeon_id, surgery_date

```sql
DELETE FROM surgeries
WHERE surgery_id = 3
```

**Output:**

<img width="1683" height="503" alt="image" src="https://github.com/user-attachments/assets/4df908ff-c0ff-4a9e-89ee-c42298f0213d" />


**Question 9**
---
Write a SQL query to find all employees who were hired on a weekend (Saturday or Sunday) from the emp table

emp table

| cid | name     | type          |
|-----|----------|---------------|
| 0   | empno    | INT           |
| 1   | ename    | VARCHAR(100)  |
| 2   | job      | VARCHAR(50)   |
| 3   | mgr      | INT           |
| 4   | hiredate | DATE          |
| 5   | sal      | DECIMAL(10,2) |
| 6   | comm     | DECIMAL(10,2) |
| 7   | deptno   | INT           |    

```sql
SELECT ename,hiredate,strftime('%w',hiredate) AS day_of_week
FROM emp
WHERE strftime('%w',hiredate) IN ('0','6');
```

**Output:**

<img width="997" height="397" alt="image" src="https://github.com/user-attachments/assets/11a6ae6e-3477-46a6-954d-86ca087e8543" />


**Question 10**
---
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.

```sql
UPDATE purchases
SET per_unit_price = 25,total_price = quantity * 25
WHERE purchase_date = '2022-08-15' AND product_id = 12;
```

**Output:**

<img width="1787" height="407" alt="image" src="https://github.com/user-attachments/assets/1f10ea07-a96a-4d68-baa8-d23b44612bf8" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
