[[SQL]]
[[Company Database into]]

## Find all branches and their manager
```sql
SELECT employee.emp_id, employee.first_name, brabch.branch_name
From employee
join branch
ON employee.emp_id = branch.mgr_id;
```

---

You're right, visualizing the output is key to understanding joins! Unfortunately, I can't execute SQL queries or display visual tables directly. 

However, let's simulate example data and then I'll describe what the output of each join would look like based on this data:

**Example Data**

**Table: Employee**

| emp_id | first_name | last_name | dept_id | branch_id |
|---|---|---|---|---|
| 1 | Alice  | Jones   | 101      | 1        |
| 2 | Bob    | Smith   | 102      | 2        |
| 3 | Charlie| Brown   | 101      | 1        |
| 4 | David  | Wilson  | 103      | NULL     |

**Table: Branch**

| branch_id | branch_name | mgr_id |
|---|---|---|
| 1        | Main St.   | 1       |
| 2        | Oak Ave.   | 2       |
| 3        | Pine Ln.   | NULL     |

**Table: Department**

| dept_id | dept_name     |
|---|---|
| 101      | Marketing   |
| 102      | Finance     |
| 103      | Human Resources |


**SQL Join Examples with Output Descriptions**

**1. INNER JOIN**

```sql
SELECT 
    e.first_name, e.last_name,
    b.branch_name,
    d.dept_name
FROM Employee e
INNER JOIN Branch b ON e.branch_id = b.branch_id
INNER JOIN Department d ON e.dept_id = d.dept_id;
```

**Output (Conceptual):**

| first_name | last_name | branch_name | dept_name  |
|---|---|---|---|
| Alice      | Jones      | Main St.    | Marketing  |
| Bob        | Smith      | Oak Ave.    | Finance    |
| Charlie    | Brown      | Main St.    | Marketing  | 

* Only employees who have a matching branch_id in the Branch table and a matching dept_id in the Department table are included.
* David (emp_id 4) is not included because he doesn't have a branch assigned (branch_id is NULL).


**2. LEFT JOIN**

```sql
SELECT 
    e.first_name, e.last_name,
    b.branch_name 
FROM Employee e
LEFT JOIN Branch b ON e.branch_id = b.branch_id;
```

**Output (Conceptual):**

| first_name | last_name | branch_name |
|---|---|---|
| Alice      | Jones      | Main St.    |
| Bob        | Smith      | Oak Ave.    |
| Charlie    | Brown      | Main St.    |
| David      | Wilson     | NULL        | 

* All employees from the Employee table are included.
* David has a `NULL` branch_name because he is not assigned to a branch.


**3. RIGHT JOIN**

```sql
SELECT 
    b.branch_name,
    e.first_name, e.last_name AS manager_name
FROM Branch b
RIGHT JOIN Employee e ON b.mgr_id = e.emp_id; 
```

**Output (Conceptual):**

| branch_name | first_name | manager_name |
|---|---|---|
| Main St.    | Alice      | Jones         |
| Oak Ave.    | Bob        | Smith         |
| Pine Ln.    | NULL       | NULL          |

* All branches from the Branch table are included.
* 'Pine Ln.' has `NULL` values for first_name and manager_name because there is no manager (Employee) assigned to it.


**4. FULL JOIN** 

```sql
SELECT 
    e.first_name, e.last_name,
    b.branch_name
FROM Employee e
FULL JOIN Branch b ON e.branch_id = b.branch_id; 
```

**Output (Conceptual):**

| first_name | last_name | branch_name |
|---|---|---|
| Alice      | Jones      | Main St.    |
| Bob        | Smith      | Oak Ave.    |
| Charlie    | Brown      | Main St.    |
| David      | Wilson     | NULL        |
| NULL       | NULL       | Pine Ln.    | 

* All employees and all branches are included.
* David has no branch, and 'Pine Ln.' has no assigned employee. 
