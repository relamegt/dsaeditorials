# SQL Data Types

In SQL, every column in a table must have a specific type of data assigned to it. This is called a **Data Type**. Choosing the right data type ensures your database stays fast, saves space, and prevents errors.

## 1. Numeric Data Types

Numeric types are used to store numbers. They are divided into two categories: **Exact** (for whole numbers and decimals) and **Approximate** (for scientific calculations).

### Exact Numbers

Use these when you need precision, such as for money or counting.

| Data Type | Description | Best Used For... |
| --- | --- | --- |
| **BIGINT** | Very large integers. | Massive IDs or global populations. |
| **INT** | Standard whole numbers. | General purpose counting and IDs. |
| **SMALLINT** | Smaller integers. | Data where numbers are rarely huge. |
| **TINYINT** | Very small integers (0-255). | Status codes or small counts. |
| **DECIMAL** | Precise fixed-point numbers. | Money and financial transactions. |
| **NUMERIC** | Similar to DECIMAL. | High-precision calculations. |

### Approximate Numbers

Use these for scientific data where the exact decimal is less important than the overall scale.

| Data Type | Description | Best Used For... |
| --- | --- | --- |
| **FLOAT** | Large floating-point numbers. | Scientific measurements. |
| **REAL** | Double-precision floating-point. | Large-scale scientific data. |

---

## 2. Character and String Types

These types are used to store text, such as names, addresses, or descriptions.

### Standard Text

Used for standard English-based characters.

| Data Type | Description | Example Use Case |
| --- | --- | --- |
| **CHAR** | Fixed-length text (pads with spaces). | Country codes (e.g., "US", "UK"). |
| **VARCHAR** | Variable-length text (saves space). | Names, emails, cities. |
| **VARCHAR(MAX)** | Large variable text. | Long bios or comments. |
| **TEXT** | Massive blocks of text data. | Article content or descriptions. |

### Unicode Text

Use these if your application needs to support international languages (like Hindi, Arabic, or Chinese) or emojis.

| Data Type | Description | Best Used For |
| --- | --- | --- |
| **NCHAR** | Fixed-length Unicode text. | International fixed codes. |
| **NVARCHAR** | Variable-length Unicode. | Global names and addresses. |
| **NVARCHAR(MAX)** | Large Unicode text. | International content. |

---

## 3. Date and Time Types

These types are essential for tracking events, birthdays, and system logs.

| Data Type | Description | Storage Size |
| --- | --- | --- |
| **DATE** | Stores Year, Month, and Day. | Birthdays, holidays. |
| **TIME** | Stores Hour, Minute, and Second. | Daily schedules. |
| **DATETIME** | Stores both Date and Time. | Transaction logs and timestamps. |

---

## 4. Binary Data Types

Binary types store "raw" data that isn't readable as text, like images or encrypted files.

| Data Type | Description | Max Length |
| --- | --- | --- |
| **BINARY** | Fixed-length binary data. | 8000 bytes |
| **VARBINARY** | Variable-length binary data. | 8000 bytes |
| **VARBINARY(MAX)** | Large binary data. | Up to 2GB |
| **IMAGE** | Legacy type for images. | (Use VARBINARY instead) |

---

## 5. Special and Logic Types

These are used for logic and advanced mapping.

| Type | Description | Usage |
| --- | --- | --- |
| **BOOLEAN** | Logical True/False. | Often stored as 1 (True) or 0 (False). |
| **XML** | Structured web data. | Configuration files. |
| **GEOMETRY** | Planar/spatial data. | Maps, GPS coordinates, and shapes. |

![SQL Data types](https://raw.githubusercontent.com/relamegt/dsaeditorials/main/images/sql-data-types/1781437240201-sql_datatypes.png)

---

### Quick Summary Table

| If you want to store... | Use this Data Type... |
| --- | --- |
| **Whole Numbers** | `INT`, `BIGINT` |
| **Prices / Money** | `DECIMAL`, `NUMERIC` |
| **Names / Titles** | `VARCHAR` |
| **International Text** | `NVARCHAR` |
| **Timestamps** | `DATETIME` |
| **Images / Files** | `VARBINARY(MAX)` |



###
