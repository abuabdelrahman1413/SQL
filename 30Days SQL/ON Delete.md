[[SQL]]
[[Company Database into]]

المشكلة لو حذفت صف من جدول الموظفين الجدول بيشير لمفتاح في جدول الأقسام هذه ==صعوبة الحذف==

## ON DELETE SET NULL
```sql
CREATE TABLE IF NOT EXISTS branch(

branch_id INT PRIMARY KEY,

branch_name VARCHAR(40),

mgr_id INT,

mgr_start_date DATE,

FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL

);
```
معناه لو حذفت ال emp_id في جدول الموظفين قيمة mgr_id  حتبقى NULL

## ON DELETE CASCADE
```sql
CREATE TABLE IF NOT EXISTS branch_supplier(

branch_id INT,

suplier_name VARCHAR(40),

supply_type VARCHAR(40),

PRIMARY KEY(branch_id, suplier_name),

FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
);
```
<span style="background:#fff88f">if i delete branch_id it will delete all rows contain that branch_id</span>
Let's clarify the difference between `SET NULL` and `SET CASCADE` in the context of SQL foreign key constraints. 

**In Simple Terms:**

* **`SET NULL`:** Imagine you have two tables connected by a relationship. If you delete a row from the "parent" table, `SET NULL` will automatically update the corresponding "child" rows by setting the foreign key column to `NULL`.  

* **`SET CASCADE`:**  With `SET CASCADE`, deleting a row from the "parent" table will automatically delete all related "child" rows in the related table.

**Example:**

Let's say you have an `Orders` table and a `Customers` table. The `Orders` table has a foreign key `customer_id` referencing the `Customers` table.

1. **`SET NULL` on `customer_id` in the `Orders` table:** If you delete a customer from the `Customers` table, all orders belonging to that customer will have their `customer_id` set to `NULL`. The orders remain in the database but are no longer associated with a specific customer.

2. **`SET CASCADE` on `customer_id` in the `Orders` table:** If you delete a customer from the `Customers` table, all orders associated with that customer will also be automatically deleted from the `Orders` table. 

**Primary Key vs. Not Primary Key:**

You are not entirely correct that you can only use `SET NULL` for non-primary key columns.  The choice of `SET NULL` or `SET CASCADE` **depends on the relationship you want to enforce**, not whether the column is a primary key. You can use either option on foreign keys, regardless of whether the referenced column is a primary key.

**Choosing the Right Option:**

* **`SET NULL`:** Use this when you want to keep the related data (in the "child" table) even if the "parent" record is deleted.
* **`SET CASCADE`:** Use this when deleting the "parent" record means the related "child" records are no longer meaningful and should be removed as well.

**Important:** Always consider the implications of using `SET NULL` or `SET CASCADE` carefully before implementing them in your database. Accidental data deletion can have serious consequences! 
