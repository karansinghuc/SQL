#### Question: Write a query to find the top 5 artists whose songs appear most frequently in the Top 10 of the global_song_rank table. Display the top 5 artist names in ascending order, along with their song appearance ranking.

````SQL
WITH ap AS (
SELECT
  artist_id
  ,COUNT(*) AS appearences
FROM songs s
  INNER JOIN global_song_rank g 
    ON g.song_id = s.song_id
WHERE g.rank <= 10
GROUP BY artist_id
),

rank AS( SELECT
  artist_name
  ,DENSE_RANK() OVER (ORDER BY appearences DESC) AS density_rank
  ,RANK() OVER (ORDER BY appearences DESC) AS regular_rank
FROM ap
INNER JOIN artists a ON a.artist_id = ap.artist_id
)

SELECT 
  artist_name
  ,density_rank
FROM rank
WHERE regular_rank <= 6
ORDER BY density_rank, artist_name
````

#### Schema: 
        +------------------+        +---------------------+       +---------------------+
        |      artists     |        |        songs        |       |   global_song_rank  |
        +------------------+        +---------------------+       +---------------------+
        | artist_id (PK)   |        | song_id (PK)        |       | day (PK)            |
        | artist_name      |--------| artist_id (FK)      |-------| song_id (FK)        |
        +------------------+        +---------------------+       | rank                |
                                                                   +---------------------+

Legend:

PK: Primary Key

FK: Foreign Key


