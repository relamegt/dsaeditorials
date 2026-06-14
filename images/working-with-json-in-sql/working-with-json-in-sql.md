# Working with JSON in SQL

## Introduction

JSON (JavaScript Object Notation) is a lightweight data-interchange format used to store and exchange structured information. Modern SQL databases provide built-in support for JSON, allowing developers to store, retrieve, validate, and manipulate JSON data directly within SQL queries.

JSON support bridges the gap between relational databases and semi-structured data, making it easier to work with web applications, APIs, and NoSQL-style datasets.

---

## Why Use JSON in SQL?

Working with JSON in SQL provides several advantages:

- Store semi-structured data within relational databases.
- Easily exchange data with web and mobile applications.
- Parse and extract values from JSON documents.
- Update specific JSON properties without modifying the entire document.
- Convert relational data into JSON format for APIs.
- Import JSON data into database tables.

---

## Common JSON Functions in SQL

| Function | Purpose |
| --- | --- |
| ISJSON() | Validates whether a string contains valid JSON |
| JSON_VALUE() | Extracts a single scalar value |
| JSON_QUERY() | Extracts JSON objects or arrays |
| JSON_MODIFY() | Updates values inside JSON data |
| FOR JSON | Converts SQL query results into JSON |
| OPENJSON() | Converts JSON into relational rows and columns |

---

## Creating a Sample Database

```sql
CREATE DATABASE AlphaKnowledgeDB;
```

Select the database:

```sql
USE AlphaKnowledgeDB;
```

---

## Creating a Sample Table

```sql
CREATE TABLE Authors (
    AuthorID INT PRIMARY KEY,
    AuthorName VARCHAR(100),
    Age INT,
    Skills VARCHAR(200),
    ArticlesPublished INT
);
```

---

## Inserting Sample Records

```sql
INSERT INTO Authors
VALUES
(1, 'Akash', 22, 'Java,Python,SQL', 15),
(2, 'Abhiram', 21, 'Python,NodeJS', 12),
(3, 'Hemesh', 23, 'Java,React,SQL', 18),
(4, 'Sai', 22, 'Python,React', 10);
```

Display all records:

```sql
SELECT * FROM Authors;
```

### Output

| AuthorID | AuthorName | Age | Skills | ArticlesPublished |
| --- | --- | --- | --- | --- |
| 1 | Akash | 22 | Java,Python,SQL | 15 |
| 2 | Abhiram | 21 | Python,NodeJS | 12 |
| 3 | Hemesh | 23 | Java,React,SQL | 18 |
| 4 | Sai | 22 | Python,React | 10 |

---

## Sample JSON Document

```json
{
  "Author": {
    "Name": "Akash",
    "Age": 22,
    "Skills": [
      "Java",
      "Python",
      "SQL"
    ]
  }
}
```

---

## Example 1: Validate JSON Using ISJSON()

The ISJSON() function checks whether a string contains valid JSON data.

```sql
DECLARE @JsonData NVARCHAR(MAX);

SET @JsonData =
'{
  "Author":{
      "Name":"Akash",
      "Age":22
   }
}';

SELECT ISJSON(@JsonData) AS IsValidJson;
```

### Output

| IsValidJson |
| --- |
| 1 |

### Explanation

- Returns 1 if the string is valid JSON.
- Returns 0 if the string is invalid JSON.
- Useful before processing JSON documents.

---

## Example 2: Extract a Value Using JSON_VALUE()

The JSON_VALUE() function extracts a scalar value from a JSON document.

```sql
DECLARE @JsonData NVARCHAR(MAX);

SET @JsonData =
'{
  "Author":{
      "Name":"Akash",
      "Age":22
   }
}';

SELECT JSON_VALUE(@JsonData, '$.Author.Name') AS AuthorName;
```

### Output

| AuthorName |
| --- |
| Akash |

### Explanation

- Retrieves a single value from JSON.
- Uses JSON path expressions.
- Returns scalar values such as strings or numbers.

---

## Example 3: Extract an Array Using JSON_QUERY()

The JSON_QUERY() function extracts JSON objects or arrays.

```sql
DECLARE @JsonData NVARCHAR(MAX);

SET @JsonData =
'{
  "Author":{
      "Skills":["Java","Python","SQL"]
   }
}';

SELECT JSON_QUERY(@JsonData, '$.Author.Skills') AS Skills;
```

### Output

| Skills |
| --- |
| ["Java","Python","SQL"] |

### Explanation

- Returns JSON arrays or objects.
- Preserves JSON formatting.
- Useful for nested JSON structures.

---

## Example 4: Modify JSON Data Using JSON_MODIFY()

The JSON_MODIFY() function updates values inside a JSON document.

```sql
DECLARE @JsonData NVARCHAR(MAX);

SET @JsonData =
'{
  "Author":{
      "Name":"Akash"
   }
}';

SET @JsonData =
JSON_MODIFY(@JsonData, '$.Author.Name', 'Abhiram');

SELECT @JsonData AS ModifiedJSON;
```

### Output

```json
{
  "Author": {
    "Name": "Abhiram"
  }
}
```

### Explanation

- Updates specific JSON properties.
- Keeps the overall structure unchanged.
- Can also insert or remove values.

---

## Example 5: Convert SQL Data to JSON Using FOR JSON

The FOR JSON clause converts query results into JSON format.

```sql
SELECT *
FROM Authors
FOR JSON AUTO;
```

### Output

```json
[
  {
    "AuthorID":1,
    "AuthorName":"Akash",
    "Age":22,
    "Skills":"Java,Python,SQL",
    "ArticlesPublished":15
  }
]
```

### Explanation

- Converts rows into JSON objects.
- Commonly used when creating APIs.
- Simplifies exporting relational data.

---

## Example 6: Generate JSON with a Root Element

```sql
SELECT *
FROM Authors
FOR JSON AUTO, ROOT('AuthorsData');
```

### Output

```json
{
  "AuthorsData":[
      {
         "AuthorID":1,
         "AuthorName":"Akash"
      }
  ]
}
```

### Explanation

- Adds a custom root node.
- Creates cleaner API responses.
- Helps organize JSON output.

---

## Example 7: Convert JSON into Table Format Using OPENJSON()

The OPENJSON() function converts JSON into relational rows and columns.

```sql
SELECT *
FROM OPENJSON(
'{
  "Name":"Akash",
  "Age":22
}')
WITH (
    Name VARCHAR(50),
    Age INT
);
```

### Output

| Name | Age |
| --- | --- |
| Akash | 22 |

### Explanation

- Parses JSON data.
- Converts JSON properties into table columns.
- Makes JSON easier to query using SQL.

---

## Example 8: Reading Nested JSON Arrays

```sql
DECLARE @JsonData NVARCHAR(MAX);

SET @JsonData =
'{
  "Skills":["Java","Python","SQL"]
}';

SELECT *
FROM OPENJSON(@JsonData, '$.Skills');
```

### Output

| key | value |
| --- | --- |
| 0 | Java |
| 1 | Python |
| 2 | SQL |

### Explanation

- Reads nested JSON arrays.
- Returns array elements as rows.
- Useful for reporting and analysis.

---

## Example 9: Import JSON from an External File

```sql
DECLARE @JSON NVARCHAR(MAX);

SELECT @JSON = BulkColumn
FROM OPENROWSET(
    BULK 'C:\Data\authors.json',
    SINGLE_CLOB
) AS JsonFile;

SELECT *
FROM OPENJSON(@JSON);
```

### Explanation

- Reads JSON from external files.
- Imports JSON into SQL Server.
- Useful when migrating data from APIs or NoSQL systems.

---

## Working with JSON in Azure SQL Database

Azure SQL Database provides built-in JSON support, allowing JSON documents to be stored and queried efficiently.

### Features

- Native JSON processing support.
- Store JSON inside table columns.
- Query JSON without external tools.
- Update JSON values directly.
- High-performance JSON operations.

---

## JSON Functions in Azure SQL

### Extract a Scalar Value

```sql
SELECT JSON_VALUE(data, '$.name')
FROM Users;
```

### Extract a JSON Object

```sql
SELECT JSON_QUERY(data, '$.address')
FROM Users;
```

### Update JSON Data

```sql
UPDATE Users
SET data = JSON_MODIFY(
    data,
    '$.address.city',
    'Hyderabad'
)
WHERE UserID = 1;
```

### Convert JSON to Rows

```sql
SELECT *
FROM OPENJSON(
'{"name":"Akash","age":22}'
)
WITH (
    name VARCHAR(50),
    age INT
);
```

---

## Best Practices

- Validate JSON using ISJSON() before processing.
- Store large JSON documents using NVARCHAR(MAX).
- Use JSON_VALUE() for scalar values.
- Use JSON_QUERY() for objects and arrays.
- Avoid storing excessively large JSON documents when relational tables are more suitable.
- Create indexes on frequently accessed JSON properties when supported.

---

## Important Points

- SQL Server stores JSON as text, typically in NVARCHAR columns.
- ISJSON() validates JSON documents.
- JSON_VALUE() extracts scalar values.
- JSON_QUERY() extracts objects and arrays.
- JSON_MODIFY() updates JSON data.
- FOR JSON converts SQL results into JSON.
- OPENJSON converts JSON into tabular format.
- Azure SQL provides native JSON functionality.

---

## Conclusion

Working with JSON in SQL allows developers to combine the flexibility of semi-structured data with the reliability of relational databases. Functions such as ISJSON(), JSON_VALUE(), JSON_QUERY(), JSON_MODIFY(), FOR JSON, and OPENJSON make it easy to validate, retrieve, update, export, and import JSON data. These capabilities are especially valuable when building modern applications, integrating APIs, and handling data exchanged between different systems.



###
