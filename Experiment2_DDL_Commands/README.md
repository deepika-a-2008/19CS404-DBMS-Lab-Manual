# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Insert the following products into the Products table:

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300

```sql
INSERT INTO Products(Name,Category,Price,Stock)
VALUES('Smartphone','Electronics',800,150),('Headphones','Accessories',200,300);
```

**Output:**

<img width="482" height="247" alt="image" src="https://github.com/user-attachments/assets/36ea2518-e5a1-4ec6-9e34-6db704e2d03a" />

**Question 2**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
CREATE TABLE jobs(
job_id INTEGER,
job_title CHAR,
min_salary INTEGER default(8000),
max_salary INTEGER default(NULL)
)
```

**Output:**

<img width="528" height="225" alt="image" src="https://github.com/user-attachments/assets/1308b300-7971-4163-840d-52a1ba580ff2" />

**Question 3**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
```
sql
CREATE TABLE Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER,
OrderId INTEGER,
FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID) 
)
```

**Output:**

<img width="377" height="130" alt="image" src="https://github.com/user-attachments/assets/8335d412-2a30-4157-a059-b70334b8baf2" />

**Question 4**
---
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.
```
sql
ALTER TABLE employees ADD COLUMN salary INTEGER CHECK (salary>0);
```

**Output:**

<img width="682" height="177" alt="image" src="https://github.com/user-attachments/assets/56063dd1-3553-4f4d-b769-47649461c4a1" />

**Question 5**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
```
sql
INSERT INTO Customers(CustomerID,Name,Address) VALUES(304,'Peter Parker','Spider St')
```

**Output:**

<img width="382" height="212" alt="image" src="https://github.com/user-attachments/assets/c0c00dfc-7cea-42c3-b5cc-f2658b5afdff" />

**Question 6**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
```
sql
CREATE TABLE Products(
ProductID INTEGER PRIMARY KEY,
ProductName TEXT UNIQUE NOT NULL,
Price REAL,
StockQuantity INTEGER,
CHECK(Price>0),
CHECK(StockQuantity>=0)
)
```

**Output:**

<img width="525" height="172" alt="image" src="https://github.com/user-attachments/assets/165e9b5c-047b-4d82-8950-7451c2ded8d8" />

**Question 7**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.
```
sql
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id CHAR(4),
FOREIGN KEY (icom_id) REFERENCES company(com_id)
ON UPDATE SET NULL 
ON DELETE SET NULL
);
```

**Output:**

<img width="482" height="245" alt="image" src="https://github.com/user-attachments/assets/f333dd44-e392-484c-ad1d-35edbf1ba919" />

**Question 8**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished
```
sql
INSERT INTO Books SELECT * FROM Out_of_print_books;
```

**Output:**

<img width="768" height="182" alt="image" src="https://github.com/user-attachments/assets/46245589-535c-4495-aeda-fcfd3f9c292a" />

**Question 9**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```
sql
CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
)
```

**Output:**

<img width="683" height="290" alt="image" src="https://github.com/user-attachments/assets/d8a912a5-64d5-4a1b-aa5f-08f404dee570" />

**Question 10**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
```sql
CREATE TABLE Orders(
OrderID INTEGER,
OrderDate DATE NOT NULL,
CustomerID INTEGER,
FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
)
```

**Output:**

<img width="342" height="181" alt="image" src="https://github.com/user-attachments/assets/bc8b42b5-ef21-4ef7-a754-40f849b9e030" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
