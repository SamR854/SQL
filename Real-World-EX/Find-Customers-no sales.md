## LEFT JOIN + IS NULL
  
 ### Find users who never placed an order
 Tables: 
 Users(user_id, name) 
 Orders(order_id, user_id)

  
 SELECT u.*
 FROM Users u
 LEFT JOIN Orders o 
 ON u.user_id = o.user_id
 WHERE o.user_id IS NULL;
  
 ### Products never sold
 SELECT p.*
 FROM Products p
 LEFT JOIN Sales s 
 ON p.product_id = s.product_id
 WHERE s.product_id IS NULL;"
