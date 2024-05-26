# Advanced SQL Concepts

## Joins
Joins are used to combine rows from two or more tables based on a related column between them.

### 1. INNER JOIN
Returns records that have matching values in both tables.

Syntax:
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

Example:
```sql
SELECT students.name, courses.course_name
FROM students
INNER JOIN courses
ON students.id = courses.student_id;
```

### 2. LEFT JOIN (or LEFT OUTER JOIN)
Returns all records from the left table and the matched records from the right table. If there is no match, the result is NULL from the right side.

Syntax:
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

Example:
```sql
SELECT students.name, courses.course_name
FROM students
LEFT JOIN courses
ON students.id = courses.student_id;
```

### 3. RIGHT JOIN (or RIGHT OUTER JOIN)
Returns all records from the right table and the matched records from the left table. If there is no match, the result is NULL from the left side.

Syntax:
```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

Example:
```sql
SELECT students.name, courses.course_name
FROM students
RIGHT JOIN courses
ON students.id = courses.student_id;
```

### 4. FULL JOIN (or FULL OUTER JOIN)
Returns all records when there is a match in either left or right table records.

Syntax:
```sql
SELECT columns
FROM table1
FULL JOIN table2
ON table1.column = table2.column;
```

Example:
```sql
SELECT students.name, courses.course_name
FROM students
FULL JOIN courses
ON students.id = courses.student_id;
```

## Subqueries
A subquery is a query nested inside another query.

### 1. Subquery in SELECT
Used to return a value that will be used by the main query.

Syntax:
```sql
SELECT column1, (SELECT column2 FROM table2 WHERE condition) AS alias
FROM table1
WHERE condition;
```

Example:
```sql
SELECT name, (SELECT COUNT(*) FROM courses WHERE courses.student_id = students.id) AS course_count
FROM students;
```

### 2. Subquery in WHERE
Used to filter the result set based on the result of the subquery.

Syntax:
```sql
SELECT column1
FROM table1
WHERE column2 = (SELECT column2 FROM table2 WHERE condition);
```

Example:
```sql
SELECT name
FROM students
WHERE age = (SELECT MAX(age) FROM students);
```

## Common Table Expressions (CTEs)
A CTE is a temporary result set that you can reference within a SELECT, INSERT, UPDATE, or DELETE statement.

Syntax:
```sql
WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
    WHERE condition
)
SELECT column1, column2
FROM cte_name;
```

Example:
```sql
WITH StudentAges AS (
    SELECT name, age
    FROM students
)
SELECT name
FROM StudentAges
WHERE age > 15;
```

## Window Functions
Window functions perform calculations across a set of table rows that are related to the current row.

### 1. ROW_NUMBER()
Assigns a unique number to each row.

Syntax:
```sql
SELECT column1, ROW_NUMBER() OVER (PARTITION BY column2 ORDER BY column3) AS row_num
FROM table_name;
```

Example:
```sql
SELECT name, age, ROW_NUMBER() OVER (ORDER BY age DESC) AS row_num
FROM students;
```

### 2. RANK()
Assigns a rank to each row within a partition of a result set.

Syntax:
```sql
SELECT column1, RANK() OVER (PARTITION BY column2 ORDER BY column3) AS rank
FROM table_name;
```

Example:
```sql
SELECT name, age, RANK() OVER (ORDER BY age DESC) AS rank
FROM students;
```

### 3. DENSE_RANK()
Similar to RANK(), but assigns consecutive ranks without gaps.

Syntax:
```sql
SELECT column1, DENSE_RANK() OVER (PARTITION BY column2 ORDER BY column3) AS dense_rank
FROM table_name;
```

Example:
```sql
SELECT name, age, DENSE_RANK() OVER (ORDER BY age DESC) AS dense_rank
FROM students;
```

### 4. NTILE()
Divides rows in an ordered partition into a specified number of approximately equal groups.

Syntax:
```sql
SELECT column1, NTILE(num_buckets) OVER (ORDER BY column2) AS ntile
FROM table_name;
```

Example:
```sql
SELECT name, age, NTILE(4) OVER (ORDER BY age DESC) AS quartile
FROM students;
```

## Advanced SQL Clauses
### 1. UNION and UNION ALL
Combine the result set of two or more SELECT statements.

UNION: Removes duplicate records.
UNION ALL: Includes duplicate records.

Syntax:
```sql
SELECT column1, column2
FROM table1
UNION
SELECT column1, column2
FROM table2;
```

Example:
```sql
SELECT name, age FROM students_2023
UNION
SELECT name, age FROM students_2024;
```

### 2. INTERSECT
Returns the intersection of two SELECT statements, i.e., rows that are common to both result sets.

Syntax:
```sql
SELECT column1, column2
FROM table1
INTERSECT
SELECT column1, column2
FROM table2;
```

Example:
```sql
SELECT name, age FROM students_2023
INTERSECT
SELECT name, age FROM students_2024;
```

### 3. EXCEPT (or MINUS in some databases)
Returns rows from the first SELECT statement that are not in the second SELECT statement.

Syntax:
```sql
SELECT column1, column2
FROM table1
EXCEPT
SELECT column1, column2
FROM table2;
```

Example:
```sql
SELECT name, age FROM students_2023
EXCEPT
SELECT name, age FROM students_2024;
```

## Example Database and Advanced Queries
Let's consider an additional example table named courses in our school database.

![image](https://github.com/AmalSunny992/Basic-SQL/assets/169422802/8a51b305-e38b-45b4-b2c0-b1b9fd394c27)


## Example Queries
### Inner Join to get students and their courses:
```sql
SELECT students.name, courses.course_name
FROM students
INNER JOIN courses ON students.id = courses.student_id;
```

### Subquery to find students with more than one course:
```sql
SELECT name
FROM students
WHERE id IN (
    SELECT student_id
    FROM courses
    GROUP BY student_id
    HAVING COUNT(*) > 1
);
```

### Using CTE to find students older than the average age:
```sql
WITH AverageAge AS (
    SELECT AVG(age) AS avg_age
    FROM students
)
SELECT name, age
FROM students, AverageAge
WHERE students.age > AverageAge.avg_age;
```

### Using ROW_NUMBER() to rank students by age:
```sql
SELECT name, age, ROW_NUMBER() OVER (ORDER BY age DESC) AS row_num
FROM students;
```
