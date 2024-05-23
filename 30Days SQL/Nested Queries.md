
~~م~~ ==بيبدا بالكويري الداخلي بعدين الخارجي==
## Find names of employees with total sales over 30000 

```sql
SELECT first_name, last_name
FROM employee
WHERE emp_id IN (SELECT emp_id
FROM works_with
WHERE total_sales > 30000
);
```

## Find all clients who are handled by the branch that Michel Scott manages Assume you know Michel's id
```sql
SELECT *
FROM client
WHERE client.branch_id = (SELECT branch.branch_id
FROM branch
WHERE branch.mgr_id = 102
);
```