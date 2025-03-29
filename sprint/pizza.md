```
WITH monthlymax AS (
	SELECT MONTH(date) AS max_month
		, od.date AS max_date
        , SUM(quantity) AS quan_count
        , RANK() OVER (PARTITION BY MONTH(date) ORDER BY SUM(quantity) DESC) AS fir_rank
	FROM order_details odt
	LEFT JOIN orders od
	USING (order_id)
	GROUP BY MONTH(date), date
    )
SELECT max_month, max_date, quan_count 
FROM monthlymax
WHERE fir_rank = 1
```
