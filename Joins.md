## Question

Write a query to report the company ID which is a Supercloud customer.


````SQL
SELECT customer_id
FROM customer_contracts c
INNER JOIN products p ON c.product_id = p.product_id
GROUP BY customer_id
HAVING COUNT(DISTINCT p.product_category) = (SELECT COUNT(DISTINCT product_category) FROM products)
````

## Schema: 

![image](https://github.com/karansinghuc/SQL/assets/140108687/67d709b6-15c3-4d9a-bcdb-2127b4f1f420)


