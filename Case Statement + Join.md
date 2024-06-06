## Question  

Write a query to obtain a breakdown of the time spent sending vs. opening snaps as a percentage of total time spent on these activities grouped by age group. Round the percentage to 2 decimal places in the output.


```SQL
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
  age_bucket;
```

## Schema: 

https://github.com/karansinghuc/SQL/blob/5dac7ca384b088f2334e3507d23007a204c1e52a/Capture.JPG