[[SQL]]
## Show all table:
```sql
SELECT *
FROM student;
```

## Show just name column:
```sql
SELECT name
FROM student;
```

## Order info
```sql
SELECT name
FROM student 
ORDER BY name DESC; -- ASC
```

في الكود اللي تحت حيرتبهم أول شيء بالأسماء ثم اذا كان في أسماء متشابهة حيرتبهم بال id ثم حيجيب أول 3 عناصر
```sql 
SELECT *
FROM student
ORDER BY major, student_id LIMIT 3;
-- <>  not equal
```

<span style="background:#b1ffff">DESC تنازلي</span>
<span style="background:#b1ffff">ASC  تصاعدي</span>

## condition in group
```sql
SELECT *
FROM student
WHERE major IN ("CS", "BIO");
```

