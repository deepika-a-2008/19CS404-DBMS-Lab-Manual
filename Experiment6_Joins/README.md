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
-- Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a date of birth after '1990-01-01'.

```sql
SELECT p.first_name AS patient_name, d.first_name AS doctor_name 
FROM PATIENTS p 
INNER JOIN DOCTORS d
ON p.doctor_id = d.doctor_id 
WHERE p.discharge_date > '1990-01-01';
```

**Output:**

<img width="745" height="347" alt="image" src="https://github.com/user-attachments/assets/aee31691-ee6a-4966-ad28-e28d28ece097" />

**Question 2**
---
-- Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.

```sql
select p.first_name, s.surgery_id, p.patient_id, s.surgeon_id, s.surgery_date 
FROM PATIENTS p
INNER JOIN SURGERIES s 
ON p.patient_id = s.patient_id 
WHERE p.discharge_date BETWEEN '2024-03-01' AND '2024-03-31';
```

**Output:**

<img width="1254" height="433" alt="image" src="https://github.com/user-attachments/assets/edeb9409-107e-4e07-944b-dbd3c78ed0b1" />

**Question 3**
---
-- From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.
```sql
SELECT c.cust_name AS "Customer Name", c.city, s.name as Salesman, s.commission 
FROM customer c 
JOIN salesman s 
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1262" height="802" alt="image" src="https://github.com/user-attachments/assets/2f2c91fa-4d1d-418a-81e3-1e984fea3c83" />

**Question 4**
---
-- Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column.


```sql
SELECT c.cust_name, o.ord_no, o.ord_date, o.purch_amt 
FROM CUSTOMER c
LEFT JOIN ORDERS o
ON c.customer_id = o.customer_id;
```

**Output:**

<img width="1254" height="785" alt="image" src="https://github.com/user-attachments/assets/cbc9ae2d-830d-4091-8c29-c4b9bf377ca2" />

**Question 5**
---
-- write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.


```sql
SELECT s.name AS "Salesman", c.cust_name, s.city 
FROM salesman s, customer c
WHERE s.city = c.city;
```

**Output:**

<img width="1061" height="645" alt="image" src="https://github.com/user-attachments/assets/507235b3-667d-4227-82f0-7dc06900c64a" />

**Question 6**
---
-- Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the specialization from the "doctors" table (aliased as "Doctor_specialization"), with an inner join on the "doctor_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.


```sql
SELECT p.first_name AS "patient_name", d.specialization AS "Doctor_specialization" 
FROM PATIENTS p 
INNER JOIN DOCTORS d 
ON p.doctor_id = d.doctor_id 
WHERE p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**

<img width="729" height="350" alt="image" src="https://github.com/user-attachments/assets/4a354b39-d74b-4073-9390-5153165e8a93" />

**Question 7**
---
-- Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned.


```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, c.cust_name, c.city AS "customer_city", c.grade, s.name AS "salesman_name", s.city AS "salesman_city", s.commission
FROM orders o 
INNER JOIN customer c
ON o.customer_id = c.customer_id 
INNER JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1255" height="780" alt="image" src="https://github.com/user-attachments/assets/48150b27-0f97-4119-bfcd-a56549e91312" />

**Question 8**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.


```sql
-- SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name AS "name",
    s.commission
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
LEFT JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1247" height="784" alt="image" src="https://github.com/user-attachments/assets/5b4d7918-a068-4d9a-bf70-2b701b093b52" />

**Question 9**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman_id values that have more than one associated customer.


```sql
SELECT 
    s.name, 
    c.cust_name, 
    c.city, 
    c.grade, 
    c.salesman_id
FROM 
    customer c
LEFT JOIN 
    salesman s ON c.salesman_id = s.salesman_id
WHERE 
    c.salesman_id IN (
        SELECT 
            salesman_id 
        FROM 
            customer 
        GROUP BY 
            salesman_id 
        HAVING 
            COUNT(customer_id) > 1
    )
ORDER BY 
    c.salesman_id, c.customer_id;

```

**Output:**

<img width="1255" height="639" alt="d5fa612e-5b9b-4c3a-8f44-14d4bc183227" src="https://github.com/user-attachments/assets/56f92048-580d-414c-a415-c253390a4c33" />

**Question 10**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.


```sql
-- SELECT o.ord_no, o.purch_amt, c.cust_name, c.city 
FROM orders o
INNER JOIN customer c
ON o.customer_id = c.customer_id 
WHERE o.purch_amt BETWEEN 500 AND 2000
ORDER BY o.ord_no;
```

**Output:**

<img width="1254" height="510" alt="68f60cc2-b16d-4cf2-81c6-775097ddaf68" src="https://github.com/user-attachments/assets/c3719079-8326-46fd-b12f-f1b3316e7168" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
