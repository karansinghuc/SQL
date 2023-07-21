## Question

Write a query to obtain a breakdown of the time spent sending vs. opening snaps as a percentage of total time spent on these activities grouped by age group. Round the percentage to 2 decimal places in the output.


````SQL
SELECT 
  age_bucket,
    ROUND(
      100*SUM(CASE WHEN activity_type = 'send' THEN time_spent ELSE 0 END) / SUM(time_spent)
      ,2)AS send_perc,
    ROUND(
      100*SUM(CASE WHEN activity_type = 'open' THEN time_spent ELSE 0 END) / SUM(time_spent)
      ,2) AS open_perc
  
FROM activities a 
INNER JOIN age_breakdown ab
  ON a.user_id = ab.user_id
WHERE activity_type IN ('open','send')
GROUP BY 
  age_bucket
````

Schema: 

![image](https://github.com/karansinghuc/SQL/assets/140108687/3ad63f45-9a96-4a83-97f3-43a83f194278)
