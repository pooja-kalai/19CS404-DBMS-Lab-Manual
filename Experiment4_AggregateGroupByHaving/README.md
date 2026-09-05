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
<img width="1033" height="251" alt="image" src="https://github.com/user-attachments/assets/eef0976f-7533-40ee-8999-d1da1e297dec" />

```
select Address ,count(*) as TotalPatients from Patients group by Address;
```

**Output:**
<img width="757" height="427" alt="image" src="https://github.com/user-attachments/assets/fa38a9e4-4661-4315-b77d-4c203f3bf5a0" />

**Question 2**
<img width="1007" height="225" alt="image" src="https://github.com/user-attachments/assets/2369dfe5-6fb1-4cd9-b32b-048494f2abd8" />


```
select PatientID, count(*)  as TotalMedications from Prescriptions group by PatientID;
```

**Output:**

<img width="712" height="762" alt="image" src="https://github.com/user-attachments/assets/2b08c20d-58d1-4051-8cc3-8fc5874f8960" />


**Question 3**

What is the average duration of insurance coverage for patients covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
StartDate          DATE
EndDate            DATE

```
select InsuranceCompany,avg(EndDate-StartDate) as AvgCoverageDurationDays from Insurance group by InsuranceCompany;
```

**Output:**

<img width="897" height="672" alt="image" src="https://github.com/user-attachments/assets/78e2fe60-4cfd-4efd-a860-f4a2c8253f0e" />


**Question 4**

Write a SQL query to find the total number of unique cities in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER

```
select count(distinct city) as unique_cities from customer;
```

**Output:**

<img width="480" height="297" alt="image" src="https://github.com/user-attachments/assets/5f6be1c4-a547-4edb-b5f6-8842b83169fa" />

**Question 5**

<img width="946" height="282" alt="image" src="https://github.com/user-attachments/assets/7cdd4c3d-4648-41b4-8d87-e2da0270acfd" />


```
select count(*) as COUNT from customer where city!='Noida';

```

**Output:**
<img width="380" height="307" alt="image" src="https://github.com/user-attachments/assets/bd574212-084a-4f68-b07f-3980b7a5585e" />


**Question 6**

Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```
select avg(income) as avg_income from employee where name like 'A%';
```

**Output:**

<img width="407" height="312" alt="image" src="https://github.com/user-attachments/assets/96934236-447c-446d-9ee9-857dc02140a2" />


**Question 7**

Write a SQL query to find  how many employees work in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

```
select count(*) as employees_in_california from employee where city='California';
```

**Output:**

<img width="640" height="317" alt="image" src="https://github.com/user-attachments/assets/56a91da0-4b25-4564-824e-d0e7d9d117f9" />


**Question 8**
---

<img width="1162" height="260" alt="image" src="https://github.com/user-attachments/assets/726aa94d-4f7c-4d96-a05d-e8984431a3a6" />

```
select (age/5)*5 as age_group, min(salary) as "MIN(salary)" from customer1 group by (age/5)*5 having min(salary)<2000;
```

**Output:**

<img width="613" height="321" alt="image" src="https://github.com/user-attachments/assets/af889d63-8aec-471e-b702-876f5240476b" />


**Question 9**
---

<img width="1188" height="275" alt="image" src="https://github.com/user-attachments/assets/bd16ee06-c35d-4b3f-ac5d-165c780d57b4" />


```select category_id, sum(price) as Total_Cost from products group by category_id having Total_Cost>50;
```

**Output:**

<img width="600" height="341" alt="image" src="https://github.com/user-attachments/assets/8e73b7a0-3279-4ecd-bc0b-4c3000761ca6" />


**Question 10**
---

<img width="1221" height="261" alt="image" src="https://github.com/user-attachments/assets/d0eb3d43-9907-4573-94f6-4ed9e00d62c0" />



```
select jdate,max(workhour) as "MAX(workhour)" from employee1 group by jdate having max(workhour)>12;
```

**Output:**

<img width="652" height="377" alt="image" src="https://github.com/user-attachments/assets/e049a822-59ef-4f8b-8c35-5aa2d2b5a66c" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
