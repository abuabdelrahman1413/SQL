[[SQL]]
[[Company Database into]]

## Find a list of employee in branch name
<span style="background:#fff88f">الشرط انو لازم يكون الاثنين نفس عدد الأعمدة وبرضو لازم يكونو نفس نوع البيانات</span>
```sql
SELECT first_name
FROM employee
UNION
SELECT branch_name
FROM branch;
```
