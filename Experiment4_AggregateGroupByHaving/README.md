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
<img width="877" height="265" alt="image" src="https://github.com/user-attachments/assets/9e474a56-3e88-4816-b2d7-068f1d8040e9" />

```sql
SELECT DoctorID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;
```

**Output:**


<img width="640" height="543" alt="image" src="https://github.com/user-attachments/assets/ebdeb709-d144-48bf-91cb-1117515680e5" />

**Question 2**
---
What is the total number of appointments scheduled for each day?

Table: Appointments

name                 type
-------------------  ----------
AppointmentID        INTEGER
PatientID            INTEGER
DoctorID             INTEGER
AppointmentDateTime  DATETIME
Purpose              TEXT
Status               TEXT

```sql
SELECT DATE(AppointmentDateTime) AS AppointmentDate, COUNT(*) AS TotalAppointments FROM Appointments
GROUP BY DATE(AppointmentDateTime)
ORDER BY AppointmentDate;
```

**Output:**


<img width="721" height="556" alt="image" src="https://github.com/user-attachments/assets/7c613f78-f6ae-40b9-972c-cfd734bc5037" />

**Question 3**
---

<img width="875" height="245" alt="image" src="https://github.com/user-attachments/assets/3708f7c1-49e9-45cd-8bb9-0aa1e7a93b53" />

```sql
SELECT Specialty, COUNT(*) AS TotalDoctors FROM Doctors
GROUP BY Specialty
ORDER BY Specialty;
```

**Output:**


<img width="687" height="607" alt="image" src="https://github.com/user-attachments/assets/957f342b-ab8e-4707-9dbf-05d69ff6a6bd" />

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
```sql
SELECT AVG(LENGTH(email)) AS avg_email_length
FROM customer;
```

**Output:**


<img width="492" height="238" alt="image" src="https://github.com/user-attachments/assets/828e24cc-3566-47bc-b6e0-5cd61d0381c0" />

**Question 5**
---
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```sql
SELECT name AS Employee_Name, age AS Age FROM employee
WHERE age=(SELECT MIN(age) FROM employee) LIMIT 1;
```

**Output:**


<img width="590" height="237" alt="image" src="https://github.com/user-attachments/assets/0c92abc3-5059-46c5-a43b-8d6c0f200f78" />

**Question 6**
---
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```sql
SELECT SUM(purch_amt) AS TOTAL
FROM orders;
```

**Output:**


<img width="357" height="252" alt="image" src="https://github.com/user-attachments/assets/029cb74c-16ce-4660-b002-d7e655a307a0" />

**Question 7**
---
Write a SQL query to find the total number of unique cities in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
```sql
SELECT COUNT(DISTINCT city) AS unique_cities
FROM customer;
```

**Output:**


<img width="393" height="247" alt="image" src="https://github.com/user-attachments/assets/6645162a-c27a-4f9b-a10d-260493f8d6a9" />

**Question 8**
---

<img width="806" height="321" alt="image" src="https://github.com/user-attachments/assets/20af72a5-7dd9-416a-8b18-46dfa299cc9c" />

```sql
SELECT city, SUM(income) AS Income FROM employee
GROUP BY City HAVING SUM(income)>200000;
```

**Output:**


<img width="535" height="457" alt="image" src="https://github.com/user-attachments/assets/efa03965-acb7-4f99-a872-ad70d0e307a8" />

**Question 9**
---

<img width="831" height="286" alt="image" src="https://github.com/user-attachments/assets/c28ab864-d558-43bd-ae5a-6d2f55499fe8" />

```sql
SELECT (age/5)*5 AS age_group, MIN(salary)
FROM customer1
GROUP BY (age/5)*5
HAVING MIN(salary)<2000;
```

**Output:**


<img width="562" height="277" alt="image" src="https://github.com/user-attachments/assets/a81643f0-1bf8-4f90-97b8-c55c35c949b8" />

**Question 10**
---

<img width="807" height="296" alt="image" src="https://github.com/user-attachments/assets/e33c7e4f-5136-4ae1-97f4-878d107189d5" />

```sql
SELECT address, SUM(salary) FROM customer1 GROUP BY address HAVING SUM(salary)>2000;
```

**Output:**


<img width="541" height="420" alt="image" src="https://github.com/user-attachments/assets/f67ae228-a409-4271-9289-4ef1bfa0d793" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
