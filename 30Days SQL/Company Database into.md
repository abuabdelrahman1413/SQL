[[SQL]]
## Target Database
![[Pasted image 20240522091504.png]]
## Create employee table
```sql
CREATE TABLE IF NOT EXISTS employee(

emp_id INT PRIMARY KEY,

first_name VARCHAR(40),

last_name VARCHAR(40),

birth_day DATE,

sex VARCHAR(1),

salary INT,

super_id INT,

branch_id INT

);
```



## Create branch table
```sql
CREATE TABLE IF NOT EXISTS branch(

branch_id INT PRIMARY KEY,

branch_name VARCHAR(40),

mgr_id INT,

mgr_start_date DATE,

FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL

);

```

## Set Foreign key for employee table
```sql
ALTER TABLE employee

ADD FOREIGN KEY (branch_id)

REFERENCES branch(branch_id)

ON DELETE SET NULL;

  

ALTER TABLE employee

ADD FOREIGN KEY (super_id)

REFERENCES employee(emp_id)

ON DELETE SET NULL;
```

## Create client table
```sql
CREATE TABLE IF NOT EXISTS client(

client_id INT PRIMARY KEY,

client_name VARCHAR(40),

branch_id INT,

FOREIGN KEY (branch_id) REFERENCES branch(branch_id) ON DELETE SET NULL

);
```

## Create works with table
```sql
CREATE TABLE IF NOT EXISTS works_with(

emp_id INT,

client_id INT,

PRIMARY KEY(emp_id, client_id),

FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE,

FOREIGN KEY(client_id) REFERENCES client(client_id) ON DELETE CASCADE

);
```

## Create branch_suplier table
```sql
CREATE TABLE IF NOT EXISTS branch_supplier(

branch_id INT,

suplier_name VARCHAR(40),

supply_type VARCHAR(40),

PRIMARY KEY(branch_id, suplier_name),

FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE

);
```

## How insert data very complex
```sql
INSERT INTO employee VALUES (100, "Dvid", "Washington", '1999-01-01', 'M', 25000, NULL, NULL);

INSERT INTO branch VALUES (1, "Main", 100, '2006-02-19');

  

UPDATE employee

SET branch_id = 1

WHERE emp_id = 100;

  

INSERT INTO employee VALUES (101, "John", "Doe", '1999-01-01', 'M', 30000, NULL, NULL);

INSERT INTO branch VALUES (2, "Branch2", 101, '2006-02-19');

  

UPDATE employee

SET branch_id = 2

WHERE emp_id = 101;

SELECT * FROM employee;

SELECT * FROM branch;

INSERT INTO employee VALUES (102, "Jane", "John", '1993-04-22', 'M', 2000, 100, NULL);

INSERT INTO branch VALUES (3, "Branch3", 102, '2006-02-19');

  

UPDATE employee

SET branch_id = 3

WHERE emp_id = 102;

  

INSERT INTO employee VALUES (103 , "Mike", "Jones", '1998-05-01', 'M', 25000, 101, NULL);

INSERT INTO branch VALUES (4, "Branch4", 103, '2006-02-19');

  

UPDATE employee

SET branch_id = 4

WHERE emp_id = 103;

  
  

INSERT INTO employee VALUES (104, "Mary", "Brown", '1995-06-15', 'F', 32000, 102, NULL);

INSERT INTO branch VALUES (5, "Branch5", 104, '2006-02-19');

  

UPDATE employee

SET branch_id = 5

WHERE emp_id = 104;

  

INSERT INTO employee VALUES (105, "David", "Smith", '2000-07-01', 'M', 28000, 103, NULL);

INSERT INTO branch VALUES (6, "Branch6", 105, '2006-02-19');

  

UPDATE employee

SET branch_id = 6

WHERE emp_id = 105;

  

INSERT INTO employee VALUES (106, "Linda", "Williams", '2002-08-15', 'F', 35000, 104, NULL);

INSERT INTO branch VALUES (7, "Branch7", 106, '2006-02-19');

  

UPDATE employee

SET branch_id = 7

WHERE emp_id = 106;

  

INSERT INTO employee VALUES (107, "Christopher", "Johnson", '2003-09-22', 'M', 40000, 105, NULL);

INSERT INTO branch VALUES (8, "Branch8", 107, '2006-02-19');

  

UPDATE employee

SET branch_id = 8

WHERE emp_id = 107;

  

INSERT INTO employee VALUES (108, "Jennifer", "Brown", '2004-10-01', 'F', 45000,102, NULL);

INSERT INTO branch VALUES (9, "Branch9", 108, '2006-02-19');

  

UPDATE employee

SET branch_id = 9

WHERE emp_id = 108;

  
  
  

SELECT * FROM employee;

SELECT * FROM branch;

  

INSERT INTO branch_supplier VALUES (2, "Hammer Mill", "Paper");

INSERT INTO branch_supplier VALUES (2, "Uni-ball", "Writing Utensils");

INSERT INTO branch_supplier VALUES (3, "Hammer Mill", "Paper");

INSERT INTO branch_supplier VALUES (3, "Uni-ball", "Writing Utensils");

  

INSERT INTO client VALUES (400, "Dunmore Highschool", 2);

INSERT INTO client VALUES (401, "Lackawana Country", 2);

INSERT INTO client VALUES (402, "FedEx", 3);

INSERT INTO client VALUES (403, "John Dalyers", 3);

INSERT INTO client VALUES (404, "Scranton Whitepages", 2);

INSERT INTO client VALUES (405, "Times Newspaper", 3);

  

ALTER TABLE works_with

ADD COLUMN total_sales INT;

  
  

INSERT INTO works_with VALUES (105, 400, 55000);

INSERT INTO works_with VALUES (102, 401, 267000);

INSERT INTO works_with VALUES (108, 402, 22500);

INSERT INTO works_with VALUES (107, 403, 5000);

INSERT INTO works_with VALUES (108, 403, 12000);

  

SHOW COLUMNS FROM works_with;

  

SELECT * FROM employee;

SELECT * FROM branch;

SELECT * FROM client;

SELECT * FROM works_with;

SELECT * FROM branch_supplier;
```