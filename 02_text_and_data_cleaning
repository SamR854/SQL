# Text & Data Cleaning

## Overview

Data cleaning is one of the most common tasks performed by Data Analysts and BI Analysts.

Before data can be analysed, it often needs to be:

- Standardised
- Reformatted
- Converted to the correct data type
- Cleaned of unwanted characters
- Prepared for reporting and dashboarding


## Commonly Used Functions
### Requirement	          |    	### Function
Remove spaces	            |     TRIM()
Convert to uppercase	    |    	UPPER()
Convert to lowercase	    |    	LOWER()	        |    
Replace text	            |    	REPLACE()
Regex cleaning	          |    	REGEXP_REPLACE()
Convert data types	      |    	CAST()
Safe conversion	          |    	SAFE_CAST()
Replace NULL values	      |    	IFNULL()
Combine fields	          |    	CONCAT()
Extract part of a string	|    	SUBSTR()
Remove duplicate records	|    	DISTINCT
Count unique values	      |    	COUNT(DISTINCT)
------------------------------------------------------------------------
These examples demonstrate common SQL data-cleaning techniques used in reporting, analytics, dashboard development, and ETL processes.


## Key Learning Outcome

After mastering these functions, you should be comfortable:

- Cleaning text fields
- Standardising categories - Handling NULL values
- Converting data types
- Removing duplicates
- Preparing datasets for reporting *nd analysis

These functions appear routinely in BigQuery, SQL Server* Snowflake, Redshift, PostgreSQL and Databricks SQL environments.


---

# Example 1: Remove Leading and Trailing Spaces

### SQL

SELECT
    TRIM(CustomerName) AS customer_name
FROM Customers;

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

SELECT
    UPPER(CustomerName) AS customer_name
FROM Customers;

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

SELECT
    LOWER(CustomerName) AS customer_name
FROM Customers;

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

SELECT
    REPLACE(channel, 'Paid Search', 'PPC') AS channel
FROM MarketingData;

### Explanation

Replaces one text value with another.

Example:

Paid Search

Becomes:

PPC

Useful for:

- Standardising marketing channels
- Renaming categories
- Cleaning inconsistent source data

---

# Example 5: Regex Cleaning

### SQL

SELECT
    REGEXP_REPLACE(
        channel,
        r'\s[/-]\s.*',
*       ''
    ) AS cleaned_channel * FROM MarketingData;
```

### Explanation

Removes everything * appearing after:

*- 

or

 /
*``

Examples: 
Email - Pro*o*```
Becomes:  Email*```

Display / Retarget*ng
Becomes: Display

Commonly used when standardising channel names.

---
*# Example*6: Convert Text to Number

### SQL*
SELECT
    CAST(Amount AS NUMERIC) AS amount
FROM Sales

### Explanation

Converts text values into numbers.

Required before:

- SUM()
- AVG()
- Mathematical calculations

# Example 7: Safe Data Type Conversion

### SQL

SELECT *   
  SAFE_CAST(AmountText AS NUMERIC) AS amount
FROM Sales;

### Explanation

Unlike CAST(), SAFE_CAST() won't fail if the value cannot be convertyed.

Very useful when dealing with messy source data.

---

# Example 8: Replace NULL Values

## SQL

SELECT
    IFNULL(channel, 'Unknown') AS channel
FROM MarketingData;


### Explanation

Replaces NULL values with a default value.
Useful in reports and dashboards.

---

# Example 9: Combine Fields

### SQL

```sql*SELECT
    CONCAT(first_name, ' ',*last_name) AS full_name
FROM Customers;
```

### Explanation

Combines multiple fields into one.
Example:

John
*mith

Becomes: *ohn Smith

Frequently used in reporting datasets.

# Example 10: Extract Part of a String

### SQL

SELECT
    SUBSTR(product_code, 1, 3) AS product_type
FROM Products;


### Explanation
Extracts part of a string

Example:

MOT12345*``` 
Returns: M*T

Useful when codes contain category information*

---

# Example 11: Remove Duplicate*Records

### SQL

SELECT DISTINCT
    customer_id*
    customer_name
FROM Customers;

### Explanation

Returns uniqUe records only.

Example:

Before:
1001  John Smith
1001  John Smith
1002  Jane Doe

After:

1001  John Smith
1002  Jane Doe 

Useful when exploring new datasets.


# Example 12: CounT Unique Values

### SQL

SELECT
    COUNT(DISTINCT customer_id) AS unique_customers
FROM Orders;

### Explanation

Counts unique Values instead of total rows.

Example:

Order Count = 1500
Unique Customers = 600

Common Business question:

> How many unique customers purchased this month?

``*
