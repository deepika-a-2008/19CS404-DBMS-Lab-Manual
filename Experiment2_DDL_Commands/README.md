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
<img width="922" height="371" alt="image" src="https://github.com/user-attachments/assets/2401ae9a-95e2-4ee2-bd35-1d5a399a7aac" />

```sql
INSERT INTO Products(Name,Category,Price,Stock)
VALUES('Smartphone','Electronics',800,150),('Headphones','Accessories',200,300);
```

**Output:**

<img width="915" height="250" alt="image" src="https://github.com/user-attachments/assets/33156f20-aa9e-4215-971d-8b322f16646a" />


**Question 2**
---
<img width="1205" height="240" alt="image" src="https://github.com/user-attachments/assets/23de0bd9-a6f7-41cd-a9fc-4e61835f6984" />

```sql
CREATE TABLE jobs(
job_id INTEGER,
job_title CHAR,
min_salary INTEGER default(8000),
max_salary INTEGER default(NULL)
)
```

**Output:**

<img width="1030" height="225" alt="image" src="https://github.com/user-attachments/assets/0b14528d-5698-46d2-a7aa-0fb94386e37d" />

**Question 3**
---

```sql
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

<img width="725" height="130" alt="image" src="https://github.com/user-attachments/assets/2dad092f-c71a-4a34-b902-dc6bae036bfd" />

**Question 4**
---

```sql
ALTER TABLE employees ADD COLUMN salary INTEGER CHECK (salary>0);
```

**Output:**

<img width="1162" height="181" alt="image" src="https://github.com/user-attachments/assets/02c73860-9716-444e-ad48-85fa8e11bb2d" />

**Question 5**
---
<img width="1003" height="416" alt="image" src="https://github.com/user-attachments/assets/7a1a2035-842b-4c70-94a4-67893c173a61" />

```sql
INSERT INTO Customers(CustomerID,Name,Address) VALUES(304,'Peter Parker','Spider St')
```

**Output:**

<img width="1073" height="222" alt="image" src="https://github.com/user-attachments/assets/a61b482f-c0d1-4785-afc8-31a4bf9be0e7" />

**Question 6**
---
<img width="1198" height="342" alt="image" src="https://github.com/user-attachments/assets/e76b6856-50ad-48dc-a79b-8c88ab6ab8b6" />

```sql
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

<img width="1036" height="173" alt="image" src="https://github.com/user-attachments/assets/b28a5afa-7c82-4bb7-8983-61e23a9d5b3d" />

**Question 7**
---
<img width="1043" height="447" alt="image" src="https://github.com/user-attachments/assets/97aa4069-7796-453f-a126-cab91abc1305" />

```sql
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

<img width="945" height="247" alt="image" src="https://github.com/user-attachments/assets/236405f7-5649-4c0f-a367-a490017b337a" />

**Question 8**
---
<img width="1005" height="351" alt="image" src="https://github.com/user-attachments/assets/23971342-14dd-4a00-bb29-a28febb4314e" />

```sql
INSERT INTO Books SELECT * FROM Out_of_print_books;
```

**Output:**

<img width="776" height="183" alt="image" src="https://github.com/user-attachments/assets/7abadb6d-6268-4711-9a06-48ac7bb28e4b" />

**Question 9**
---
<img width="1068" height="455" alt="image" src="https://github.com/user-attachments/assets/733b37ee-e34a-451d-88d3-f1cd8b6723f2" />

```sql
CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
)
```

**Output:**

<img width="693" height="302" alt="image" src="https://github.com/user-attachments/assets/837e1dcd-e894-4d59-aac6-98f56a6c60c7" />

**Question 10**
---
<img width="1137" height="316" alt="image" src="https://github.com/user-attachments/assets/0c44c721-5b28-4aaf-bc2f-ff3c11d99e8b" />

```sql
CREATE TABLE Orders(
OrderID INTEGER,
OrderDate DATE NOT NULL,
CustomerID INTEGER,
FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
)
```

**Output:**

<img width="722" height="178" alt="image" src="https://github.com/user-attachments/assets/6b3262c2-d717-4cfe-bd43-75e3ea8447b0" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
