Orders-by-customer.md

## GROUP BY
### Count orders per day
 SELECT order_date, COUNT(*) AS total_orders
 FROM Orders
 GROUP BY order_date;
  
###  Count orders per customer
 SELECT customer_id, COUNT(*) AS total_orders
 FROM Orders
 GROUP BY customer_id;
  
###  Total spend per customer
 SELECT customer_id, SUM(amount) AS total_spend
 FROM Orders
 GROUP BY customer_id; 
  
###  How many employees are in each department.
 SELECT dept, COUNT(*) AS total_employees
 FROM Employees
 GROUP BY dept;"
