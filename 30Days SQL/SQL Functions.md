[[SQL]]
[[Company Database into]]

## Find num of employee
```sql
SELECT COUNT(emp_id)
FROM employee;
```

## Find num of employee hav super_id
```sql 
SELECT COUNT(super_id)
FROM employee
```

## Find num of female employee born after 1970
```sql
SELECT COUNT(emp_id)
FROM employee
WHERE sex = 'f' AND birth_day > '1970-01-01'
```

## Find avg salary of males
```sql
SELECT AVG(salary)
FROM employee
WHERE sex = "m";
```

## Find sum of salary
```sql
SELECT SUM(salary)
FROM employee;
```

## Find how many male and female
```sql
SELECT COUNT(sex), sex
FROM employee
GROUP BY sex;
```

##  Find total sales of each salesman
```sql 
SELECT SUM(total_sales),emp_id 
FROM works_with
GROUP BY emp_id;
```