# SQL Nested Queries

## Introduction

A Nested Query (also known as a Subquery) is a query written inside another SQL query. The inner query executes first and its result is used by the outer query.

Nested queries help simplify complex database operations such as filtering, comparison, aggregation, and data retrieval from related tables.

### Why Use Nested Queries?

- Retrieve data based on another query's result.
- Simplify complex filtering conditions.
- Work with related tables efficiently.
- Perform comparisons using dynamic values.
- Support data modification operations.

---

## Syntax

```sql
SELECT column_name
FROM table_name
WHERE column_name OPERATOR
(
    SELECT column_name
    FROM table_name
    WHERE condition
);
```

### Syntax Components

| Component | Description |
| --- | --- |
| Outer Query | Main query executed after subquery |
| Inner Query | Query executed first |
| Operator | IN, NOT IN, ANY, ALL, EXISTS, etc. |
| Condition | Filtering criteria |

---

## Creating Sample Tables

### STUDENT Table

```sql
CREATE TABLE STUDENT (
    S_ID INT PRIMARY KEY,
    S_NAME VARCHAR(100),
    S_ADDRESS VARCHAR(100),
    S_PHONE VARCHAR(15),
    S_AGE INT
);
```

### COURSE Table

```sql
CREATE TABLE COURSE (
    C_ID VARCHAR(10) PRIMARY KEY,
    C_NAME VARCHAR(100)
);
```

### STUDENT_COURSE Table

```sql
CREATE TABLE STUDENT_COURSE (
    S_ID INT,
    C_ID VARCHAR(10)
);
```

---

## Sample Data

```sql
INSERT INTO STUDENT VALUES
(1,'Akash','Hyderabad','9876543210',21),
(2,'Rahul','London','9876543211',20),
(3,'Sai','Mumbai','9876543212',22),
(4,'Daniel','Chennai','9876543213',24);
```

```sql
INSERT INTO COURSE VALUES
('C1','DSA'),
('C2','DBMS'),
('C3','Java');
```

```sql
INSERT INTO STUDENT_COURSE VALUES
(1,'C1'),
(2,'C2'),
(3,'C3'),
(4,'C1');
```

---

## Types of Nested Queries

### 1. Independent Nested Query

The inner query executes independently and passes its result to the outer query.

#### Example 1: Using IN

Find students enrolled in DSA or DBMS.

```sql
SELECT S_ID
FROM STUDENT_COURSE
WHERE C_ID IN
(
    SELECT C_ID
    FROM COURSE
    WHERE C_NAME IN ('DSA','DBMS')
);
```

### Explanation

- Inner query retrieves course IDs.
- Outer query retrieves student IDs enrolled in those courses.

### Output

| S_ID |
| --- |
| 1 |
| 2 |
| 4 |

### 2. Correlated Nested Query

The inner query depends on values from the outer query.

#### Example 2: Using EXISTS

Find students enrolled in course C1.

```sql
SELECT S_NAME
FROM STUDENT S
WHERE EXISTS
(
    SELECT 1
    FROM STUDENT_COURSE SC
    WHERE S.S_ID = SC.S_ID
    AND SC.C_ID = 'C1'
);
```

### Explanation

- The subquery checks each student individually.
- Students enrolled in C1 are returned.

### Output

| S_NAME |
| --- |
| Akash |
| Daniel |

---

## Common Operators Used with Nested Queries

### 1. IN Operator

Checks whether a value exists in a list returned by a subquery.

#### Example

```sql
SELECT S_NAME
FROM STUDENT
WHERE S_ID IN
(
    SELECT S_ID
    FROM STUDENT_COURSE
    WHERE C_ID IN
    (
        SELECT C_ID
        FROM COURSE
        WHERE C_NAME IN ('DSA','DBMS')
    )
);
```

### Explanation

- Retrieves students enrolled in DSA or DBMS.

### Output

| S_NAME |
| --- |
| Akash |
| Rahul |
| Daniel |

---

### 2. NOT IN Operator

Returns values not present in the subquery result.

#### Example

```sql
SELECT S_ID
FROM STUDENT
WHERE S_ID NOT IN
(
    SELECT S_ID
    FROM STUDENT_COURSE
    WHERE C_ID IN
    (
        SELECT C_ID
        FROM COURSE
        WHERE C_NAME IN ('DSA','DBMS')
    )
);
```

### Explanation

- Finds students not enrolled in DSA or DBMS.

### Output

| S_ID |
| --- |
| 3 |

---

### 3. ANY Operator

Returns TRUE if the condition matches at least one value.

#### Example

```sql
SELECT S_NAME
FROM STUDENT
WHERE S_AGE > ANY
(
    SELECT S_AGE
    FROM STUDENT
    WHERE S_ADDRESS = 'London'
);
```

### Explanation

- Returns students older than at least one London student.

---

### 4. ALL Operator

Returns TRUE only if the condition matches all values.

#### Example

```sql
SELECT S_NAME
FROM STUDENT
WHERE S_AGE > ALL
(
    SELECT S_AGE
    FROM STUDENT
    WHERE S_ADDRESS = 'London'
);
```

### Explanation

- Returns students older than every London student.

---

## Nested Query vs Correlated Query

| Nested Query | Correlated Query |
| --- | --- |
| Executes once | Executes for each row |
| Independent | Depends on outer query |
| Faster | Usually slower |
| Easier to optimize | More dynamic |

---

## Advantages of Nested Queries

- Simplifies complex SQL statements.
- Improves readability.
- Supports dynamic filtering.
- Useful with aggregation functions.
- Works well with related tables.

---

## Best Practices

- Keep nesting levels minimal.
- Use meaningful aliases.
- Optimize with indexes.
- Consider JOINs for better performance.
- Test queries on large datasets.

---

## Important Points

- Inner query executes before the outer query.
- Nested queries can be used in SELECT, WHERE, FROM, and HAVING clauses.
- IN, EXISTS, ANY, and ALL are commonly used operators.
- Correlated queries are a special type of nested query.
- Nested queries help solve complex filtering requirements.

---

## Conclusion

SQL Nested Queries allow one query to use the result of another query, making complex data retrieval easier and more efficient. They are widely used for filtering, comparisons, aggregation, and working with related tables. Understanding nested queries is essential for writing powerful and flexible SQL statements.



###
