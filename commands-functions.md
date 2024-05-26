# Basic SQL Commands and Functions

## Basic SQL Commands

### 1. SELECT
Used to retrieve data from a database.
Syntax:
```sql
SELECT column1, column2, ...
FROM table_name;
```
**Example** :
```sql
SELECT name, age
FROM students;
```
### 2. INSERT
Used to insert new records into a table.
Syntax:
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```
Example:
```sql
INSERT INTO students (name, age, grade)
VALUES ('John Doe', 15, '10th');
```

### 3. UPDATE
Used to modify existing records in a table.
Syntax:
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
Example:
```sql
UPDATE students
SET age = 16
WHERE name = 'John Doe';
```

### 4. DELETE
Used to delete records from a table.
Syntax:
```sql
DELETE FROM table_name
WHERE condition;
```
Example:
```sql
DELETE FROM students
WHERE name = 'John Doe';
```

### 5. CREATE TABLE
Used to create a new table.
Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```
Example:
```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    grade VARCHAR(10)
);
```

### 6. DROP TABLE
Used to delete a table and all of its data.
Syntax:
```sql
DROP TABLE table_name;
```
Example:
```sql
DROP TABLE students;
```

## Basic SQL Functions

### 1. COUNT
Returns the number of rows that match a specified criterion.
Syntax:
```sql
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```
Example:
```sql
SELECT COUNT(id)
FROM students
WHERE age > 14;
```
### 2. SUM
Returns the total sum of a numeric column.
```sql
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```
Example:
```sql
SELECT SUM(age)
FROM students;
```
### 3. AVG
Returns the average value of a numeric column.
Syntax:
```sql
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```
Example:
```sql
SELECT AVG(age)
FROM students;
```
### 4. MIN
Returns the smallest value in a column.
Syntax:
```sql
SELECT MIN(column_name)
FROM table_name
WHERE condition;
```
Example:
```sql
SELECT MIN(age)
FROM students;
```

### 5. MAX
Returns the largest value in a column.

Syntax:
```sql
SELECT MAX(column_name)
FROM table_name
WHERE condition;
```
Example:
```sql
SELECT MAX(age)
FROM students;
```
## Basic SQL Clauses

### 1. WHERE
Filters records based on a specified condition.
Syntax:
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
Example:
```sql
SELECT name, age
FROM students
WHERE grade = '10th';
```

### 2. ORDER BY
Sorts the result set in ascending or descending order.
Syntax:
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 ASC|DESC, column2 ASC|DESC, ...;
```
Example:
```sql
SELECT name, age
FROM students
ORDER BY age DESC;
```

### 3. GROUP BY
Groups rows that have the same values into summary rows.
Syntax:
```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1;
```
Example:
```sql
SELECT grade, COUNT(*)
FROM students
GROUP BY grade;
```

### 4. HAVING
Filters records that are returned by a GROUP BY clause.
Syntax:
```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1
HAVING condition;
```
Example:
```sql
SELECT grade, COUNT(*)
FROM students
GROUP BY grade
HAVING COUNT(*) > 1;
```

## Example Database and Queries
Let's consider a simple example database named school with a table students.

![image](https://github.com/AmalSunny992/Basic-SQL/assets/169422802/6871ba23-78b2-4952-a74b-12c9cdfab029)


### Example Queries

#### Select all students:
```sql
SELECT * FROM students;
```

#### Select students who are in the 10th grade:
```sql
SELECT name, age FROM students WHERE grade = '10th';
```

#### Update age of a student:
```sql
UPDATE students SET age = 17 WHERE name = 'Lisa White';
```

#### Delete a student record:
```sql
DELETE FROM students WHERE name = 'Sam Brown';
```

#### Count the number of students in each grade:
```sql
SELECT grade, COUNT(*) FROM students GROUP BY grade;
```

#### Find the average age of students:
```sql
SELECT AVG(age) FROM students;
```
