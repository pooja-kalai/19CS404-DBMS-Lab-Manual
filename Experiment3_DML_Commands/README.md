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
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.

```
update purchases
set per_unit_price = 25, total_price=25*quantity
where purchase_date='2022-08-15' and product_id=12;
```

**Output:**

<img width="1241" height="617" alt="image" src="https://github.com/user-attachments/assets/a072c83e-9edd-4d9d-8a8f-169f3dca6a4f" />


**Question 2**
---
Write a SQL statement to Change the category to 'Household' where product name contains 'Detergent' in the products table.

Products Table

name type

product_id INT PRIMARY KEY
product_name VARCHAR(10) category VARCHAR(50) cost_price DECIMAL(10) sell_price DECIMAL(10) reorder_lvl INT
quantity INT
supplier_id INT

```
update products
set category='Household'
where product_name LIKE '%Detergent%';
```

**Output:**

<img width="1243" height="593" alt="image" src="https://github.com/user-attachments/assets/69d3dbd2-1286-4316-8b1a-9be92a342b3f" />


**Question 3**
---
Decrease the reorder level by 30 percent where the product name contains 'cream' and quantity in stock is higher than reorder level in the products table.

PRODUCTS TABLE

name type

product_id INT product_name VARCHAR(100) category VARCHAR(50) cost_price DECIMAL(10,2) sell_price DECIMAL(10,2) reorder_lvl INT quantity INT supplier_id INT
```
update products
set reorder_lvl = reorder_lvl-(reorder_lvl*0.3)
where product_name LIKE '%cream%' and quantity>reorder_lvl;
```

**Output:**

<img width="1243" height="600" alt="image" src="https://github.com/user-attachments/assets/be6b63fc-ec50-4e7a-8a35-312670f1f47c" />


**Question 4**
---
Change the supplier name to upper case where contact person contains ' Singh' in suppliers table.

name type

supplier_id INT supplier_name VARCHAR(100) contact_person VARCHAR(100) phone_number VARCHAR(20) email VARCHAR(100) address VARCHAR(250)

```
update suppliers
set supplier_name= UPPER(supplier_name)
where contact_person LIKE '%Singh%';
```

**Output:**
<img width="1236" height="442" alt="image" src="https://github.com/user-attachments/assets/516421aa-a799-45ca-ae2f-a2813d6699db" />



**Question 5**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

product_id product_name category_id availability

```
update products
set product_name= 'Grapefruit'
where product_id = 4;
```

**Output:**
<img width="1238" height="336" alt="image" src="https://github.com/user-attachments/assets/bb3a8338-3665-477e-8d6c-59cf3b14cdc8" />



**Question 6**
---
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```
delete from doctors
where specialization IS NULL;
```

**Output:**

<img width="1312" height="833" alt="image" src="https://github.com/user-attachments/assets/4eb73f6d-0e41-44fe-b23c-2ffd627624c4" />


**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is exactly 2.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
|CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO | AGENT_CODE | +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+ | C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 | | C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 | | C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 |

```
delete from customer
where grade==2;
```

**Output:**
<img width="1306" height="498" alt="image" src="https://github.com/user-attachments/assets/7b4bb64e-53e5-44f7-9898-5a8fe733955c" />



**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'WORKING_AREA' is 'New York'.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
|CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO | AGENT_CODE | +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+ | C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 | | C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 | | C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 | For example:

```
delete from customer
where working_area = 'New York';
```

**Output:**

<img width="1306" height="680" alt="image" src="https://github.com/user-attachments/assets/799ea91b-878e-4862-b96e-2a35a54f9b65" />


**Question 9**
---
Write a SQL query to Delete customers from 'customer' table where 'OPENING_AMT' is between 4000 and 6000.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
|CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO | AGENT_CODE | +-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+ | C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 | | C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 | | C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 |

```
delete from customer
where opening_amt between 4000 and 6000;
```

**Output:**

<img width="1306" height="555" alt="image" src="https://github.com/user-attachments/assets/5181452b-6f60-4746-b798-b7ace08b2ef7" />


**Question 10**
---
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
```
delete from doctors
where specialization='Cardiology';
```

**Output:**




<img width="1302" height="347" alt="image" src="https://github.com/user-attachments/assets/dabc3213-ec65-4263-9472-07b98999fe73" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
