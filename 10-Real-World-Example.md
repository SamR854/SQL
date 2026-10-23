
## Common Questions From Stakeholders

1. How many orders do we receive each month?
2. How many unique customers purchase each month?
3. Is revenue increasing or decreasing?
4. What is the month-on-month growth percentage?
5. Which customers generate the most revenue?
6. Which products sell the most?
7. What is the average order value?
8. How long does it take to complete an order?
9. Are there duplicate records?
10. Are there missing or invalid values affecting reporting?

# Real World Example: Analysing Order Data

## Scenario

You receive a table called `orders` containing:

```text
order_id
order_date
completion_date
customer_id
product_id
order_value
```

Before building reports or dashboards, you should validate the data.

---

## Step 1: Check for Duplicate Orders

Duplicate records can inflate revenue and order counts.

```sql
SELECT
    order_id,
    COUNT(*) AS*duplicate_count
FROM orders
GROUP *Y order_id
HAVING COUNT(*) > 1;
```

---

## Step 2: Check for Missing Values

Missing dates or customer IDs can impact reporting.

```sql
SELECT *
FROM orders
WHERE order_date IS NULL
   OR customer_id IS NULL
   OR order_value IS NULL;
```

---

## Step 3: Check Date Ranges

Confirm that the data contains the period you expect.

```sql
SELECT
    MIN(order_date) AS first_order,
    MAX(order_date) AS last_order
FROM orders;
```

---

## Step 4: Check for Negative or Zero Values

```sql
SELECT *
FROM orders
WHERE order_value <= 0;
```

---

## Step 5: Count Orders and Customers by Month

This is often the first KPI requested by the business.

```sql
SELECT
    FORMAT(CAST(order_date AS DATE), 'yyyy-MM') AS month,
    COUNT(order_id) AS total_orders,
    COUNT(DISTINCT customer_id) AS total_customers
FROM orders
GROUP BY FORMAT(CAST(order_date AS DATE), 'yyyy-MM')
ORDER BY month;
```

Expected Output:

| month | total_orders | total_customers |
|---------|---------|---------|
| 2024-01 | 1250 | 890 |
| 2024-02 | 1380 | 940 |
| 2024-03 | 1425 | 987 |

---

## Step 6: Monthly Revenue

```sql
SELECT
    FORMAT(CAST(order_date AS DATE), 'yyyy-MM') AS month,
    SUM(order_value) AS revenue
FROM orders
GROUP BY FORMAT(CAST(order_date AS DATE), 'yyyy-MM')
ORDER BY month;
```

---

## Step 7: Month-on-Month Revenue Comparison

Use the `LAG()` window function to compare against the previous month.

```sql
WITH monthly_sales AS
(
    SELECT
        FORMAT(CAST(order_date AS DATE), 'yyyy-MM') AS month,
        SUM(order_value) AS revenue
    FROM orders
    GROUP BY FORMAT(CAST(order_date AS DATE), 'yyyy-MM')
)

SELECT
    month,
    revenue,
    LAG(revenue) OVER (ORDER BY month) AS previous_month_revenue,
    revenue -
        LAG(revenue) OVER (ORDER BY month) AS revenue_difference
FROM monthly_sales
ORDER BY month;
```

---

## Step 8: Month-on-Month Percentage Growth

This is one of the most common dashboard metrics.

```sql
WITH monthly_sales AS
(
    SELECT
        FORMAT(CAST(order_date AS DATE), 'yyyy-MM') AS month,
        SUM(order_value) AS revenue
    FROM orders
    GROUP BY FORMAT(CAST(order_date AS DATE), 'yyyy-MM')
)

SELECT
    month,
    revenue,
    LAG(revenue) OVER (ORDER BY month) AS previous_month_revenue,

    ROUND(
        (
            revenue -
            LAG(revenue) OVER (ORDER BY month)
        ) * 100.0
        /
        NULLIF(
            LAG(revenue) OVER (ORDER BY month),
            0
        ),
        2
    ) AS growth_percentage
FROM monthly_sales
ORDER BY month;
```

Expected Output:

| month | revenue | previous_month_revenue | growth_percentage |
|---------|---------|---------|---------|
| 2024-01 | 100000 | NULL | NULL |
| 2024-02 | 115000 | 100000 | 15.00 |
| 2024-03 | 127500 | 115000 | 10.87 |

---

## Date Formatting Notes

Different SQL databases store dates differently.

If `order_date` is already a date field, you can use:

```sql
FORMAT(CAST(order_date AS DATE), 'yyyy-MM')
```

Example:

```sql
SELECT
    FORMAT(CAST(order_date AS DATE), 'yyyy-MM') AS month,
    COUNT(*) AS total_orders
FROM*orders
GROUP BY FORMAT(CAST(order_*ate AS DATE), 'yyyy-MM');
```

---*
If your date is stored as*a string in the format:

```text
2*240115*```

you may need to convert it fi*st*

```sql
SELECT
    CAST(
        *ONCAT(
            SUBSTR(CAST(ord*r_date AS STRING*,1,4),
            '-',
          **SUBSTR(CAST(order_date AS STRING),*,2),
            '-',
            *UBSTR(CAST(order_date AS STRING),7*2)
        ) AS TIMESTAMP
    ) AS*formatted_date
FROM orders;
```

O*tput*

```text
20240115
```

*ecomes

```text
2024*01-15 00:00:00*```

You can then use the formatte**date in reporting:

```sql
SELECT
*   FORMAT(
        CAST(
         *  CONCAT(
                SUBSTR*CAST(order_date AS STRING*,1,4),
                '-',
      *         SUBSTR(CAST(order_date AS*STRING),5,2),
                '-',*                SUBSTR(CAST*order_date AS STRING),7,2)
       *    ) AS TIMESTAMP
        ),
    *   'yyyy-MM'
    ) AS month,
    COUNT(*) AS total_orders
FROM orders
GROUP BY month
ORDER BY month;
```

---

### Tip

Always check the data type first:

```sql
SELECT *
FROM orders
LIMIT 10;
```

Questions to ask:

- Is the date already a DATE field?
- Is it a TIMESTAMP?
- Is it stored as text?
- Is it in `YYYYMMDD` format?
- Does it contain invalid dates?

Date issues are one of the most common causes of reporting errors.
