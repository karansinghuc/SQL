## Question

Assume you're given a table containing data on Amazon customers and their spending on products in different categorie, write a query to identify the top two highest-grossing products within each category in the year 2022. The output should include the category, product, and total spend.

````SQL
SELECT category, product,total_spend
FROM 
  (SELECT 
    category
    ,product
    ,SUM(spend) as total_spend
    ,RANK() OVER (PARTITION BY category ORDER BY SUM(spend) DESC) AS rank 
  FROM product_spend
  WHERE date_part('year',transaction_date) = 2022
  GROUP BY category,product) sub
WHERE rank IN (1,2)
````

## Schema: 

![image](https://github.com/karansinghuc/SQL/assets/140108687/b29bb59e-c8ed-40c7-98b9-37d87d6cf549)

