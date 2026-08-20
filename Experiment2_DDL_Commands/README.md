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
```
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      
```

### sql code:
```
INSERT INTO Customers (CustomerID, Name, Address)
VALUES (304, 'Peter Parker', 'Spider St');
```

**Output:**

<img width="1236" height="407" alt="1" src="https://github.com/user-attachments/assets/1e1745e1-37f1-4699-aa5d-b0338e7157b7" />



**Question 2**
```
Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
```

### sql code:


```
ALTER TABLE Student_details
ADD COLUMN Country TEXT;
```

**Output:**
<img width="1251" height="457" alt="2" src="https://github.com/user-attachments/assets/be3a3c6b-d6ea-4bf2-9d43-56e4d6243f13" />


**Question 3**
```
Create a table named Bonuses with the following constraints:

- BonusID as INTEGER should be the primary key.
- EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
- BonusAmount as REAL should be greater than 0.
- BonusDate as DATE.
- Reason as TEXT should not be NULL.
```

### sql code:

```
CREATE TABLE Bonuses (
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK (BonusAmount > 0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1255" height="446" alt="4" src="https://github.com/user-attachments/assets/3c86d277-ce67-40b3-83ed-541c46822e3b" />
<img width="1233" height="372" alt="3" src="https://github.com/user-attachments/assets/f74e8218-1c96-4b2a-8847-cbd2c3734a9a" />


**Question 4**
```
Insert the following employees into the Employee table:

EmployeeID  Name        Position    Department  Salary
----------  ----------  ----------  ----------  ----------
2           John Smith  Developer   IT          75000
3           Anna Bell   Designer    Marketing   68000

```


### sql code:


```



 INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)
VALUES(2,"John Smith","Developer","IT",75000),
(3, 'Anna Bell', 'Designer', 'Marketing', 68000);

```

**Output:**

<img width="1255" height="446" alt="4" src="https://github.com/user-attachments/assets/cceeee7e-3c75-47bd-a788-886100c0e0db" />


**Question 5**
```
Create a table named Employees with the following columns:

- `EmployeeID` as `INTEGER`
- `FirstName` as `TEXT`
- `LastName` as `TEXT`
- `HireDate` as `DATE`
```

### sql code:


```
CREATE TABLE Employees (
    EmployeeID INTEGER,
    FirstName TEXT,
    LastName TEXT,
    HireDate DATE
);
```

**Output:**
<img width="1236" height="395" alt="5" src="https://github.com/user-attachments/assets/28c3dd59-0186-4166-8579-bf6f1cc98465" />



**Question 6**
```

Create a new table named contacts with the following specifications:

- `contact_id` as `INTEGER` and primary key.
- `first_name` as `TEXT` and not NULL.
- `last_name` as `TEXT` and not NULL.
- `email` as `TEXT`.
- `phone` as `TEXT` and not NULL with a check constraint to ensure the length of `phone` is at least 10 characters.

```
### sql code:


```



CREATE TABLE contacts(contact_id INTEGER PRIMARY KEY,
                      first_name TEXT NOT NULL,
                      last_name TEXT NOT NULL,
                      email TEXT,
                      phone TEXT NOT NULL CHECK (LENGTH(phone) >= 10)
);
              
```

**Output:**

<img width="1245" height="412" alt="6" src="https://github.com/user-attachments/assets/b35cbd79-9b12-4660-83cf-1a3d51138327" />


**Question 7**
```
Create a table named Employees with the following constraints:

- `EmployeeID` should be the primary key.
- `FirstName` and `LastName` should be `NOT NULL`.
- `Email` should be unique.
- `Salary` should be greater than 0.
- `DepartmentID` should be a foreign key referencing the `Departments` table.
```

### sql code:


```
CREATE TABLE Employees (
    EmployeeID INTEGER PRIMARY KEY,
    FirstName TEXT NOT NULL,
    LastName TEXT NOT NULL,
    Email TEXT UNIQUE,
    Salary REAL CHECK (Salary > 0),
    DepartmentID INTEGER,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="1238" height="527" alt="7" src="https://github.com/user-attachments/assets/919ae962-5f54-4868-9152-050e5df23a99" />


**Question 8**
```
In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375
```

### sql code:

```
INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES
(306, 'Diana Prince', 'Themyscira', NULL, NULL),
(307, 'Bruce Wayne', 'Wayne Manor', 'Gotham', 10007),
(308, 'Peter Parker', 'Queens', NULL, 11375);
```
**Output:**

<img width="1247" height="397" alt="8" src="https://github.com/user-attachments/assets/9dff7025-503e-434d-9a5c-35a92e120c46" />


**Question 9**
```
Create a table named Tasks with the following columns:

- `TaskID` as `INTEGER`
- `TaskName` as `TEXT`
- `DueDate` as `DATE`
```


### sql code:


```
CREATE TABLE Tasks (
    TaskID INTEGER,
    TaskName TEXT,
    DueDate DATE
);

```

**Output:**

<img width="1247" height="470" alt="9" src="https://github.com/user-attachments/assets/a96fe61a-4ef1-4e0a-b137-04d78e0830c5" />


**Question 10**
```
Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002

```


### sql code:
<img width="1236" height="407" alt="1" src="https://github.com/user-attachments/assets/bae7ba7f-f541-49d9-9687-c1c661191ee1" />


```
ALTER TABLE customer
ADD COLUMN birth_date timestamp;
```

**Output:**
<img width="1243" height="458" alt="10" src="https://github.com/user-attachments/assets/6b267510-1c85-41bf-a181-fc321e2c981a" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
