# Text & Data Cleaning

## Overview

Data cleaning is one of the most common tasks performed by Data Analysts and BI Analysts.

Before data can be analysed, it often needs to be:

- Standardised
- Reformatted
- Converted to the correct data type
- Cleaned of unwanted characters
- Prepared for reporting and dashboarding

---

## Commonly Used Functions

| Requirement | Function |
|------------|------------|
| Remove spaces | `TRIM()` |
| Convert to uppercase | `UPPER()` |
| Convert to lowercase | `LOWER()` |
| Replace text | `REPLACE()` |
| Convert data types | `CAST()` |
| Safe conversion | `SAFE_CAST()` |
| Replace NULL values | `IFNULL()` |
| Combine fields | `CONCAT()` |
| Extract part of a string | `SUBSTR()` |
| Remove duplicate records | `DISTINCT` |
| Count unique values | `COUNT(DISTINCT)` |
| Regex cleaning | `REGEXP_REPLACE()` |

These examples demonstrate common SQL data-cleaning techniques used in reporting, analytics, dashboard development, and ETL processes.

---

# Example 1: Remove Leading and Trailing Spaces

### SQL

```sql
SELECT
    TRIM(CustomerName) AS customer_name
FROM Customers;
```

### Explanation

Removes unnecessary spaces before and after text.

Example:

```text
' John Smith '
```

Becomes:

```text
'John Smith'
```

Useful before:

- Grouping
- Joining
- Deduplication

---

# Example 2: Convert Text to Uppercase

### SQL

```sql
SELECT
    UPPER(CustomerName) AS customer_name
FROM Customers;
```

### Explanation

Converts all text to uppercase.

Example:

```text
John
JOHN
john
```

Becomes:

```text
JOHN
JOHN
JOHN
```

Useful when standardising inconsistent text values.

---

# Example 3: Convert Text to Lowercase

### SQL

```sql
SELECT
    LOWER(CustomerName) AS customer_name
FROM Customers;
```

### Explanation

Converts all text to lowercase.

Example:

```text
John
JOHN
john
```

Becomes:

```text
john
john
john
```

Useful when matching values regardless of capitalization.

---

# Example 4: Replace Text Values

### SQL

```sql
SELECT
    REPLACE(channel, 'Paid Search', 'PPC') AS channel
FROM MarketingData;
```

### Explanation

Replaces one text value with another.

Example:

```text
Paid Search
```

Becomes:

```text
PPC
```

Useful for:

- Standardising marketing channels
- Renaming categories
- Cleaning inconsistent source data

---

# Example 5: Convert Text to Number

### SQL

```sql
SELECT
    CAST(AmountText AS NUMERIC) AS amount
FROM Sales;
```

### Explanation

Converts text values into numbers.

Example:

```text
'150'
```

Becomes:

```text
150
```

Required before:

- `SUM()`
- `AVG()`
- Mathematical calculations

---

# Example 6: Safe Data Type Conversion

### SQL

```sql
SELECT
    SAFE_CAST(AmountText AS NUMERIC) AS amount
FROM Sales;
```

### Explanation

Unlike `CAST()`, `SAFE_CAST()` will not fail if a value cannot be converted.

Example:

```text
'150'
```

Returns:

```text
150
```

Example:

```text
'ABC'
```

Returns:

```text
NULL
```

Very useful when dealing with messy source data.

---

# Example 7: Replace NULL Values

### SQL

```sql
SELECT
    IFNULL(channel, 'Unknown') AS channel
FROM MarketingData;
```

### Explanation

Replaces NULL values with a default value.

Example:

```text
NULL
```

Becomes:

```text
Unknown
```

Useful in reports and dashboards.

---

# Example 8: Combine Fields

### SQL

```sql
SELECT
    CONCAT(first_name, ' ', last_name) AS full_name
FROM Customers;
```

### Explanation

Combines multiple fields into one.

Example:

```text
John
Smith
```

Becomes:

```text
John Smith
```

Frequently used in reporting datasets.

---

# Example 9: Extract Part of a String

### SQL

```sql
SELECT
    SUBSTR(product_code, 1, 3) AS product_type
FROM Products;
```

### Explanation

Extracts part of a string.

Example:

```text
MOT12345
```

Returns:

```text
MOT
```

Useful when codes contain category information.

---

# Example 10: Remove Duplicate Records

### SQL

```sql
SELECT DISTINCT
    customer_id,
    customer_name
FROM Customers;
```

### Explanation

Returns unique records only.

Before:

```text
1001  John Smith
1001  John Smith
1002  Jane Doe
```

After:

```text
1001  John Smith
1002  Jane Doe
```

Useful when exploring new datasets.

---

# Example 11: Count Unique Values

### SQL

```sql
SELECT
    COUNT(DISTINCT customer_id) AS unique_customers
FROM Orders;
```

### Explanation

Counts unique values instead of all rows.

Example:

```text
Total Orders:      1500
Unique Customers:   600
```

Common business questions:

- How many unique customers purchased this month?
- How many unique users logged in?
- How many unique products were sold?

---

# Example 12: Regex Cleaning

### SQL

```sql
SELECT
    REGEXP_REPLACE(
        channel,
        r'\s[/-]\s.*',
        ''
    ) AS cleaned_channel
FROM MarketingData;
```

### Explanation

Removes*everything appearing after:

```te*t
 - 
```

or

```text
 /
``*

Examples:

```text
Email - Promo*```

Becomes:

```text
Email
```

*``text
Display / Retargeting
```

Becomes:

```text
Display
```

Comm*nly used when standardising channe* names and marketing source data.
*
