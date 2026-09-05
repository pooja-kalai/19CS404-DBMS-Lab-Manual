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

# PROGRAM:
```
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);
CREATE TABLE employee_log (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    log_date DATE
);
CREATE OR REPLACE TRIGGER emp_insert_log
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log
    VALUES (:NEW.emp_id, :NEW.emp_name, SYSDATE);
END;
/
INSERT INTO employees
VALUES (4, 'Gokul', 'Developer');

COMMIT;
SELECT * FROM employee_log;
```
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**

<img width="637" height="82" alt="image" src="https://github.com/user-attachments/assets/59f15f42-f42e-41ff-9921-9271c2715240" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.

# PROGRAM:
```
CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);
CREATE TABLE employee_log (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    log_date DATE
);
CREATE OR REPLACE TRIGGER emp_insert_log
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log
    VALUES (:NEW.emp_id, :NEW.emp_name, SYSDATE);
END;
/
INSERT INTO employees
VALUES (4, 'Gokul', 'Developer');

COMMIT;
SELECT * FROM employee_log;

CREATE OR REPLACE TRIGGER prevent_delete
BEFORE DELETE ON employees
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(
        -20001,
        'Deletion is not allowed from this table'
    );
END;
/
DELETE FROM employees
WHERE emp_id = 4;
```
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**

<img width="508" height="96" alt="image" src="https://github.com/user-attachments/assets/88dcb0f6-e4aa-4839-9422-bc0ef7a657ed" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.

# PROGRAM:
```
ALTER TABLE employees ADD last_modified DATE;

CREATE OR REPLACE TRIGGER update_last_modified
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSDATE;
END;
/

UPDATE employees
SET designation = 'Senior Developer'
WHERE emp_id = 4;

COMMIT;

SELECT emp_id, emp_name, designation, last_modified
FROM employees
WHERE emp_id = 4;
```

**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**

<img width="828" height="100" alt="image" src="https://github.com/user-attachments/assets/472d2927-9945-47cc-9f52-68d0195ea2be" />


---
## 4. Write a trigger to keep track of the number of updates made to a table.

# PROGRAm:
```
CREATE TABLE update_log (
    update_count NUMBER
);

INSERT INTO update_log VALUES (0);
COMMIT;

CREATE OR REPLACE TRIGGER track_updates
AFTER UPDATE ON employees
BEGIN
    UPDATE update_log
    SET update_count = update_count + 1;
END;
/

UPDATE employees
SET designation = 'Manager'
WHERE emp_id = 4;

COMMIT;

SELECT * FROM update_log;
```

**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**

<img width="292" height="107" alt="image" src="https://github.com/user-attachments/assets/f184a707-debc-4e85-9aaa-a6ab36857236" />


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.

# PROGRAM:
```
CREATE OR REPLACE TRIGGER check_emp_id
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.emp_id <= 0 THEN
        RAISE_APPLICATION_ERROR(
            -20002,
            'Employee ID must be greater than 0'
        );
    END IF;
END;
/
INSERT INTO employees
(emp_id, emp_name, designation)
VALUES
(10, 'Kumar', 'Developer');

COMMIT;

INSERT INTO employees
(emp_id, emp_name, designation)
VALUES
(-1, 'Ravi', 'Tester');

```

**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**

<img width="422" height="130" alt="image" src="https://github.com/user-attachments/assets/e5a1ec14-1fdd-40ea-b205-29a1ec95cc42" />


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
