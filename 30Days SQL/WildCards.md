[[SQL]]
[[Company Database into]]

## Find any clients who are an LLC.
```sql
SELECT * 
FROM clients
WHERE client_name LIKE '%LLC'; -- like *LLC in linux -- mean end by LLC
```

## Find any branch supplier who are in label business
```sql
SELECT *
FROM branch_supplier
WHERE supplier_name LIKE '%Label%';
```

## Find any employee born in october
```sql
SELECT *
FROM employee
WHERE birth_date LIKE '____-10%'; -- match 4 digits and then 10  then any thing
-- '_' mean 1 char
```