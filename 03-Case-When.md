# CASE WHEN

## Overview

`CASE WHEN` allows you to add conditional logic to a SQL query.

It works similarly to an IF/ELSE statement in programming languages and is commonly used to categorize, label, or transform data.

---

## Basic Syntax

```sql
SELECT
    column_name,
    CASE
        WHEN condition_1 THEN result_1
        WHEN condition_2 THEN result_2
        ELSE result_3
    END AS new_column
FROM table_name;
```

---

## Example 1: Salary Bands

```sql
SELECT
    employee_name,
    salary,
    CASE
        WHEN salary >= 100000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_band
FROM employees;
```

---

## Example 2: Customer Tiers

```sql
SELECT
    customer_id,
    total_spend,
    CASE
        WHEN total_spend >= 10000 THEN 'Gold'
        WHEN total_spend >= 5000 THEN 'Silver'
        WHEN total_spend >= 1000 THEN 'Bronze'
        ELSE 'New Customer'
    END AS customer_tier
FROM customers;
```

---

## Example 3: Order Categories

```sql
SELECT
    order_id,
    order_amount,
    CASE
        WHEN order_amount >= 1000 THEN 'Premium'
        WHEN order_amount >= 500 THEN 'Standard'
        ELSE 'Basic'
    END AS order_type
FROM orders;
```

---

## Example 4: Handling NULL Values

```sql
SELECT
    customer_name,
    CASE
        WHEN phone_number IS NULL THEN 'Missing'
        ELSE 'Available'
    END AS phone_status
FROM customers;
```

---

## Example 5: Age Groups

```sql
SELECT
    customer_name,
    age,
    CASE
        WHEN age < 18 THEN 'Under 18'
        WHEN age BETWEEN 18 AND 30 THEN '18-30'
        WHEN age BETWEEN 31 AND 50 THEN '31-50'
        ELSE '50+'
    END AS age_group
FROM customers;
```

---

## Example 6: Product Availability

```sql
SELECT
    product_name,
    stock_quantity,
    CASE
        WHEN stock_quantity = 0 THEN 'Out of Stock'
        WHEN stock_quantity < 20 THEN 'Low Stock'
        ELSE 'In Stock'
    END AS inventory_status
FROM products;
```

---

## Example 7: Employee Level

```sql
SELECT
    employee_name,
    salary,
    CASE
        WHEN salary > 100000 THEN 'Executive'
        WHEN salary > 70000 THEN 'Senior'
        WHEN salary > 40000 THEN 'Mid-Level'
        ELSE 'Junior'
    END AS employee_level
FROM employees;
```

---

## Key Takeaways

- `CASE WHEN` adds conditional logic to a query.
- Conditions are checked from top to bottom.
- The first matching condition is returned.
- `ELSE` acts as a default value.
- `END` closes the CASE statement.
- `CASE WHEN` is commonly used for categorization and reporting.
