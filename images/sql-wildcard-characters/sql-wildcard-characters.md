# SQL Wildcard Characters

Sometimes, you need to search for data in a database, but you don't know the exact value. For example, you want to find all customers whose names start with "S" or all emails that end in "@gmail.com".

In these cases, we use **Wildcards**. Wildcards are special symbols used with the `LIKE` operator to search for patterns rather than exact matches.

---

## 1. The Percent Sign (`%`)

The percent sign is the most common wildcard. It represents **zero, one, or multiple characters**. 

| Pattern | What it finds | Example Result |
| --- | --- | --- |
| `'A%'` | Anything starting with "A" | Alice, Andrew, Austin |
| `'%i'` | Anything ending with "i" | Hawaii, Kiwi, Levi |
| `'%A%'` | "A" anywhere in the text | Sarah, Mark, Dana |
| `'%ra%'` | "ra" anywhere anywhere | Brian, Sarah, Clara |

**Example Query:**

```sql
-- Finds all customers whose first name starts with A
SELECT * FROM Customers 
WHERE FirstName LIKE 'A%';
```

---

## 2. The Underscore Sign (`_`)

The underscore represents **exactly one single character**. Use this when you know the length of the string but not the specific letters.

| Pattern | What it finds | Example Result |
| --- | --- | --- |
| `'H__'` | "H" followed by exactly 2 letters | Hat, Hen, Hoz |
| `'Dan___'` | "Dan" followed by exactly 3 letters | Daniel, Dancin |
| `'_______'` | Any name with exactly 7 characters | Michael, Jessica |

**Example Query:**

```sql
-- Finds names that start with "Dan" and have 6 letters total
SELECT * FROM Customers 
WHERE FirstName LIKE 'Dan___';
```

---

## 3. Brackets (`[]`)

Brackets are used to define a **set or a range of characters** to match.

| Pattern | What it finds | Example Result |
| --- | --- | --- |
| `'[A-C]%'` | Starts with A, B, or C | Apple, Bob, Charlie |
| `'[1-9]'` | Any digit from 1 to 9 | 5, 9 |
| `'[^y-z]'` | Any character **NOT** in y or z | Apple, Zebra |

**Example Query:**

```sql
-- Finds customers starting with A, B, or C
SELECT * FROM Customers 
WHERE LastName LIKE '[A-C]%';
```

---

## 4. Summary Reference Table

Here is a quick guide to help you remember which wildcard to use:

| Wildcard | Represents | Best Used For |
| --- | --- | --- |
| `%` | Zero, one, or many characters | Searching prefixes or suffixes. |
| `_` | Exactly one character | Searching patterns with fixed lengths. |
| `[]` | Any character in a set/range | Matching specific letters or numbers. |
| `[^]` or `!` | Any character NOT in the set | Excluding specific characters. |

---

### Pro Tip: Combining Wildcards

You can mix wildcards to create very powerful search filters. 

**Example:**

```sql
-- Finds phone numbers that start with 8, have any 2 digits, and end with 5
SELECT * FROM Customers 
WHERE Phone LIKE '8__5%';
```



###
