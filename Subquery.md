## Question

Write a query to obtain the third transaction of every user. Output the user id, spend and transaction date.

````SQL
SELECT user_id,
        spend,
        transaction_date
FROM (
      SELECT
        user_id,
        spend,
        transaction_date,
        RANK () OVER (PARTITION BY user_id ORDER BY transaction_date)
      FROM transactions
      ) AS sub
WHERE rank = 3
````

## Schema: 
![image](https://github.com/karansinghuc/SQL/assets/140108687/35345193-baca-44bd-beef-0a27401bee3b)

