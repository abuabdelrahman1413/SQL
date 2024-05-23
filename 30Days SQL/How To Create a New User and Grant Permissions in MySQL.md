## Creating a New User and Granting Permissions in MySQL

Here's a comprehensive guide on how to create a new user and grant permissions in MySQL:

**1. Connect to the MySQL Server**

* **Using the command line:**
    ```bash
    mysql -u root -p
    ```
    (Replace 'root' with your MySQL root user if different, and enter the password when prompted.)

* **Using a GUI client:**
    * Select the desired database server.
    * Login using your MySQL root user credentials.

**2. Create the New User**

```sql
CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';
```

* **'new_user':** Replace with the desired username.
* **'localhost':**  Specify the hostname from which the user can connect. Use '%' for any host.
* **'password':** Replace with the desired password for the new user.

**3. Grant Permissions**

Use the `GRANT` statement to assign specific privileges to the user. Here's a breakdown of common permission types:

**Basic Permissions:**

* **SELECT:** Allows reading data from tables.
* **INSERT:** Allows adding new data to tables.
* **UPDATE:** Allows modifying existing data in tables.
* **DELETE:** Allows removing data from tables.
* **CREATE:** Allows creating new tables, databases, etc.
* **DROP:** Allows deleting existing tables, databases, etc.
* **ALTER:** Allows modifying existing tables, databases, etc.

**Example:**

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON database_name.* TO 'new_user'@'localhost';
```

* **database_name:** Replace with the name of the database you want the user to have permissions on.
* **'new_user'@'localhost':**  The user account you're granting permissions to.

**Specific Permissions:**

You can grant permissions on specific tables or columns using:

```sql
GRANT SELECT ON database_name.table_name TO 'new_user'@'localhost';
GRANT INSERT (column1, column2) ON database_name.table_name TO 'new_user'@'localhost';
```

**4. Flush Privileges**

```sql
FLUSH PRIVILEGES;
```

This command ensures that the new permissions are immediately applied.

**5. Test the User**

* Connect to the database using the new user's credentials.
* Try performing the actions you've granted permissions for.

**Important Notes:**

* **Security:** Always use strong passwords for your MySQL users.
* **Principle of Least Privilege:** Only grant users the minimum permissions they need to perform their tasks.
* **Database Structure:** If you have a complex database structure with multiple users and roles, consider using **MySQL Roles** for granular permission management.

**Example using a Role:**

```sql
-- Create a new role
CREATE ROLE 'data_reader';
-- Grant SELECT permissions to the role
GRANT SELECT ON database_name.* TO 'data_reader';
-- Assign the role to the new user
GRANT 'data_reader' TO 'new_user'@'localhost';
```

This approach allows you to manage permissions more efficiently and separate responsibilities.

This guide provides a foundational understanding of creating users and granting permissions in MySQL. Further explore the available privileges and explore advanced concepts like roles and user administration for more sophisticated security and access control.

---

<span style="background:#fdbfff">Here are more examples of granting permissions in MySQL</span>, showcasing different scenarios and functionalities:

**1. Granting Permissions on Specific Tables:**

```sql
-- Grant SELECT and INSERT permissions on the 'users' table
GRANT SELECT, INSERT ON mydatabase.users TO 'new_user'@'localhost';

-- Grant UPDATE permission on the 'products' table, but only for specific columns
GRANT UPDATE (price, description) ON mydatabase.products TO 'new_user'@'localhost';

-- Grant DELETE permission on the 'orders' table, but only for orders with a specific status
GRANT DELETE ON mydatabase.orders WHERE status = 'cancelled' TO 'new_user'@'localhost';
```

**2. Granting Permissions on Stored Procedures and Functions:**

```sql
-- Grant EXECUTE permission on a stored procedure
GRANT EXECUTE ON PROCEDURE mydatabase.calculate_total TO 'new_user'@'localhost';

-- Grant ALTER permission on a function
GRANT ALTER ON FUNCTION mydatabase.get_user_by_id TO 'new_user'@'localhost';
```

**3. Granting Permissions to Create and Manage Databases:**

```sql
-- Grant CREATE and DROP permissions on the 'mydatabase' database
GRANT CREATE, DROP ON mydatabase.* TO 'new_user'@'localhost';

-- Grant CREATE and ALTER permissions on all databases
GRANT CREATE, ALTER ON *.* TO 'new_user'@'localhost';
```

**4. Granting Permissions on Events:**

```sql
-- Grant CREATE and DROP permissions on events
GRANT CREATE, DROP EVENT ON mydatabase.* TO 'new_user'@'localhost';

-- Grant ALTER permission on a specific event
GRANT ALTER ON EVENT mydatabase.scheduled_task TO 'new_user'@'localhost';
```

**5. Granting Permissions on Views:**

```sql
-- Grant SELECT permission on a view
GRANT SELECT ON mydatabase.product_view TO 'new_user'@'localhost';

-- Grant INSERT permission on a view
GRANT INSERT ON mydatabase.user_details_view TO 'new_user'@'localhost'; 
```

**6. Granting Permissions to Use the `SHOW` Statement:**

```sql
-- Grant permission to use SHOW databases
GRANT SHOW DATABASES ON *.* TO 'new_user'@'localhost';

-- Grant permission to use SHOW tables
GRANT SHOW TABLES ON mydatabase.* TO 'new_user'@'localhost';
```

**7. Granting Permissions to Access the MySQL System Database:**

```sql
-- Grant SELECT permission on the 'mysql' database
GRANT SELECT ON mysql.* TO 'new_user'@'localhost';
```

**Important Notes:**

* **Database Name:**  Always use the correct database name in your GRANT statements.
* **User Name:**  Ensure you use the correct user name and host.
* **Specific Permissions:**  Be precise with the permissions you grant to minimize security risks.
* **Review and Monitor:** Regularly review granted permissions and adjust them as needed for ongoing security and control.

These examples provide a variety of scenarios and demonstrate the flexibility of the `GRANT` statement. Remember to tailor your permission settings according to your specific database structure, user roles, and security requirements.


---

## MySQL GRANT Statement

This tutorial will guide you on how to use the MySQL GRANT statement to assign privileges to user accounts.

### Introduction to the MySQL GRANT Statement

The `CREATE USER` statement creates a user account with no privileges. This means the user can log in to the MySQL Server but cannot perform any actions like selecting databases or querying data.

To enable the user account to interact with database objects, you need to grant it privileges. The `GRANT` statement is used to assign one or more privileges to the user account.

#### Basic Syntax:

```sql
GRANT privilege [,privilege],.. 
ON privilege_level 
TO account_name;
```

**Explanation:**

1. **`privilege`**: Specify one or more privileges after the `GRANT` keyword. If granting multiple privileges, separate them with commas.
2. **`privilege_level`**: Determines the scope of the privileges. More information on privilege levels is provided below.
3. **`account_name`**: The user account you want to grant privileges to, after the `TO` keyword.

**Important Notes:**

* To use the `GRANT` statement, you need to have the `GRANT OPTION` privilege and the privileges you are granting.
* If the system variable `read_only` is enabled, you need the `SUPER` privilege to execute the `GRANT` statement.

### MySQL Privilege Levels

MySQL supports the following privilege levels:

| Privilege Level | Description |
|---|---|
| **Global Privileges** | Apply to all databases in a MySQL Server. Use the `*.*` syntax. |
| **Database Privileges** | Apply to all objects in a specific database. Use the `ON database_name.*` syntax. |
| **Table Privileges** | Apply to all columns in a table. Use the `ON database_name.table_name` syntax. |
| **Column Privileges** | Apply to individual columns within a table. Specify the column(s) for each privilege. |
| **Stored Routine Privileges** | Apply to stored procedures and stored functions. |
| **Proxy User Privileges** | Allow one user to be a proxy for another, inheriting all the proxied user's privileges. |

### MySQL GRANT Statement Examples

#### Example 1: Creating a User and Granting Privileges

1. **Create a new user:**

```sql
CREATE USER super@localhost IDENTIFIED BY 'Secure1Pass!';
```

2. **Show the initial privileges:**

```sql
SHOW GRANTS FOR super@localhost;
```

Output:

```
+-------------------------------------------+
| Grants for super@localhost                |
+-------------------------------------------+
| GRANT USAGE ON *.* TO `super`@`localhost` |
+-------------------------------------------+
1 row in set (0.00 sec)
```

The `USAGE` privilege means the user can log in but has no other permissions.

3. **Grant all privileges on the `classicmodels` database:**

```sql
GRANT ALL ON classicmodels.* TO super@localhost;
```

4. **Show the updated privileges:**

```sql
SHOW GRANTS FOR super@localhost;
```

Output:

```
+------------------------------------------------------------------+
| Grants for super@localhost                                       |
+------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `super`@`localhost`                        |
| GRANT ALL PRIVILEGES ON `classicmodels`.* TO `super`@`localhost` |
+------------------------------------------------------------------+
2 rows in set (0.00 sec)
```

### Permissible Privileges for the GRANT Statement

The following table lists all permissible privileges that you can use for the `GRANT` and `REVOKE` statements.

| Privilege | Meaning | Level |
|---|---|---|
| `ALL [PRIVILEGES]` | Allow the user to alter and drop stored procedures or stored functions. | Global |
| `ALTER` | Allow the user to use the `ALTER TABLE` statement. | Database, Table |
| `ALTER ROUTINE` | Allow the user to create databases and tables. | Global |
| `CREATE` | Allow the user to create stored procedures and stored functions. | Database |
| `CREATE ROUTINE` | Allow the user to create a temporary table using `CREATE TEMPORARY TABLE`. | Database |
| `CREATE TABLESPACE` | Allow the user to create, alter, or drop tablespaces and log file groups. | Global |
| `CREATE TEMPORARY TABLES` | Allow the user to use the `CREATE USER`, `DROP USER`, `RENAME USER`, and `REVOKE ALL PRIVILEGES` statements. | Database |
| `CREATE USER` | Allow the user to create or modify views. | Global |
| `CREATE VIEW` | Allow the user to use the `DELETE` statement. | Database, Table |
| `DELETE` | Allow the user to execute stored routines. | Database |
| `DROP` | Allow the user to drop databases, tables, and views. | Database, Table |
| `EVENT` | Allow the user to use events for the Event Scheduler. | Database |
| `EXECUTE` | Allow the user to drop databases, tables, and views. | Database |
| `FILE` | Allow the user to have privileges to grant or revoke privileges from other accounts. | Global |
| `GRANT OPTION` | Allow the user to create or drop indexes. | Database, Table |
| `INDEX` | Allow the user to create or drop indexes. | Database, Table |
| `INSERT` | Allow the user to use the `INSERT` statement. | Database, Table |
| `LOCK TABLES` | Allow the user to query to see where the master or slave servers are. | Database |
| `PROCESS` | Allow the user to see all processes with the `SHOW PROCESSLIST` statement. | Global |
| `PROXY` | Enable user proxying. | Global |
| `REFERENCES` | Allow the user to create foreign keys. | Database, Table |
| `RELOAD` | Allow the user to use the `FLUSH` statement. | Global |
| `REPLICATION CLIENT` | Allow the user to query to see where the master or slave servers are. | Global |
| `REPLICATION SLAVE` | Allow the user to use replicate slaves to read binary log events from the master. | Global |
| `SELECT` | Allow the user to use the `SELECT` statement. | Database, Table |
| `SHOW DATABASES` | Allow the user to show all databases. | Global |
| `SHOW VIEW` | Allow the user to use the `SHOW CREATE VIEW` statement. | Database, Table |
| `SHUTDOWN` | Allow the user to use the `mysqladmin shutdown` command. | Global |
| `SUPER` | Allow the user to use other administrative operations such as `CHANGE MASTER TO`, `KILL`, `PURGE BINARY LOGS`, `SET GLOBAL`, and `mysqladmin` command. | Global |
| `TRIGGER` | Allow the user to use TRIGGER operations. | Database, Table |
| `UPDATE` | Allow the user to use the `UPDATE` statement. | Database, Table |
| `USAGE` | Equivalent to "no privileges". | Global |

### Summary

Use the MySQL `GRANT` statement to grant privileges to users. Be careful and only grant the minimum permissions required for each user role to maintain security. Regularly review and update permissions as your dat
