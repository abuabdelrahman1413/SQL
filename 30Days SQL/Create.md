[[SQL]]

# SQL | CREATE TABLE

CREATE TABLE command creates a new table in the database in SQL. In this article, we will learn about CREATE TABLE in SQL with examples and syntax.

## SQL CREATE TABLE Statement

SQL CREATE TABLE Statement is used to create a new table in a database. Users can define the table structure by specifying the column’s name and data type in the CREATE TABLE command.

This statement also allows creating a table with constraints that define the rules for the table. Users can create tables in SQL and insert data at the time of table creation.

### Syntax

To create a table in SQL,

```sql
CREATE table table_name (
    Column1 datatype (size),
    column2 datatype (size),
    ...
    columnN datatype(size)
);
```

Here `table_name` is the name of the table, `column` is the name of the column.
#### CREATE TABLE EMPLOYEE Example

In this example, we will create a table in SQL with a primary key, named “EMPLOYEE”.

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Department VARCHAR(50),
    Salary DECIMAL(10, 2)
);
```
### Create Table From Another Table

We can also use CREATE TABLE to create a copy of an existing table. In the new table, it gets the exact column definition; all columns or specific columns can be selected.

If an existing table was used to create a new table, by default the new table would be populated with the existing values from the old table.

#### Syntax:

```sql
CREATE TABLE new_table_name AS
    SELECT column1, column2, …
    FROM existing_table_name
    WHERE …;
```

#### Query:

```sql
CREATE TABLE SubTable AS
SELECT CustomerID, CustomerName
FROM Customer;
```

**Output:**

![[Pasted image 20240521141757.png]]

Note: We can use `*` instead of the column name to copy the whole table to another table.

### Important Points About SQL CREATE TABLE Statement

- CREATE TABLE statement is used to create a new table in a database.
- It defines the structure of the table including the name and datatype of columns.
- The `DESC table_name;` command can be used to display the structure of the created table.
- We can also add constraints to the table like NOT NULL, UNIQUE, CHECK, and DEFAULT.
- If you try to create a table that already exists, MySQL will throw an error. To avoid this, you can use the `CREATE TABLE IF NOT EXISTS` syntax.

### Full Example:
```sql
-- Create the 'student' table

CREATE TABLE student (

student_id INT PRIMARY KEY,

name VARCHAR(20),

major VARCHAR(20)

);

  

-- Describe the 'student' table structure

DESCRIBE student;

  

-- Add a 'gpa' column to the 'student' table

ALTER TABLE student ADD gpa DECIMAL(3,2);

  

-- Drop the 'gpa' column from the 'student' table

ALTER TABLE student DROP COLUMN gpa;

  

-- Drop the 'student' table (use with caution - all data will be lost)

DROP TABLE student;
```