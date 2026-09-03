# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

### Program:
```

CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE TABLE employee_log (
    log_id NUMBER GENERATED ALWAYS AS IDENTITY,
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER,
    log_date DATE
);

CREATE OR REPLACE TRIGGER emp_insert_log
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log
    (emp_id, emp_name, salary, log_date)
    VALUES
    (:NEW.emp_id, :NEW.emp_name, :NEW.salary, SYSDATE);
END;
/

INSERT INTO employees
VALUES (101, 'John', 30000);

INSERT INTO employees
VALUES (102, 'Alice', 35000);

INSERT INTO employees
VALUES (103, 'David', 40000);

COMMIT;

SELECT * FROM employees;
SELECT * FROM employee_log;
```
**Output:**

<img width="816" height="341" alt="image" src="https://github.com/user-attachments/assets/cd30e322-0430-4577-949f-2a0a87e33110" />


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.
### Program:
```
CREATE TABLE sensitive_data (
    id NUMBER,
    data VARCHAR2(100)
);

INSERT INTO sensitive_data VALUES (1, 'Confidential Data');
INSERT INTO sensitive_data VALUES (2, 'Private Information');

COMMIT;

CREATE OR REPLACE TRIGGER prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(
        -20001,
        'Deletion not allowed on this table.'
    );
END;
/

DELETE FROM sensitive_data
WHERE id = 1;

SELECT * FROM sensitive_data;
```

**Output:**
<img width="880" height="422" alt="image" src="https://github.com/user-attachments/assets/86821341-fdc4-4bf5-9992-3754eb6bf89a" />


---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

### Program:
```
CREATE TABLE products (
    product_id NUMBER,
    product_name VARCHAR2(50),
    price NUMBER
);

INSERT INTO products VALUES (101, 'Laptop', 50000);
INSERT INTO products VALUES (102, 'Phone', 25000);

ALTER TABLE products
ADD last_modified TIMESTAMP;

CREATE OR REPLACE TRIGGER update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/

UPDATE products
SET price = 55000
WHERE product_id = 101;

COMMIT;

SELECT * FROM products;
```

**Output:**

<img width="922" height="267" alt="image" src="https://github.com/user-attachments/assets/57598131-b905-467d-ae8b-b08cdbd8c545" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

### Program:
```
CREATE TABLE customer_orders (
    order_id NUMBER,
    customer_name VARCHAR2(50),
    amount NUMBER
);

INSERT INTO customer_orders VALUES (101, 'John', 5000);
INSERT INTO customer_orders VALUES (102, 'Alice', 7000);

CREATE TABLE audit_log (
    update_count NUMBER
);

INSERT INTO audit_log VALUES (0);

COMMIT;

CREATE OR REPLACE TRIGGER count_order_updates
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/

UPDATE customer_orders
SET amount = 5500
WHERE order_id = 101;

UPDATE customer_orders
SET amount = 7500
WHERE order_id = 102;

COMMIT;

SELECT * FROM customer_orders;

SELECT * FROM audit_log;
```

**Output:**

<img width="942" height="406" alt="image" src="https://github.com/user-attachments/assets/0de8bde5-3c4d-4fcd-86a6-93c2bcf84f9f" />


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

### Program:
```
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE OR REPLACE TRIGGER check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20001,
            'Salary below minimum threshold.'
        );
    END IF;
END;
/

INSERT INTO employees VALUES (101, 'John', 5000);

INSERT INTO employees VALUES (102, 'Alice', 2500);

SELECT * FROM employees;
```

**Output:**

<img width="983" height="433" alt="image" src="https://github.com/user-attachments/assets/f8ab16ed-8094-4447-a86f-ba6c8966394f" />


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
