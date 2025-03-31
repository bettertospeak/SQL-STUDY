### 고급 6. 월별로 피자 주문 수량이 가장 많았던 날(date)의 날짜와 총 수량을 출력해주세요.
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

* CTE 사용 (서브쿼리 활용 방식도 있지만 코드 길어짐)
* COUNT(quantity)가 아니라 SUM(quantity)
> COUNT하면 quantity 값의 갯수를 셈
* WHERE 절에 집계 함수 못 들어감 무지성으로 넣지말자
* 근데 왜 RANK를 MONTH로 집계하는거지? DATE중에 최고를 MONTH 기준으로 출력하는거 아닌가

### 고급 7. 피자별(pizza_id) 판매 수량 순위에서 피자별 판매 수량 상위 10%에 들기 위해서는 최소 몇 판이 판매가 이루어졌는지 구해주세요.
```
WITH ten_percent AS (
	SELECT pizza_id
		, SUM(quantity) AS quan
	FROM order_details
	GROUP BY pizza_id
), 
ten_count AS (
	SELECT pizza_id
		, quan
        , PERCENT_RANK() OVER(ORDER BY quan DESC) AS ten_quan
	FROM ten_percent
)
SELECT MIN(quan) AS least_quan
FROM ten_count
WHERE ten_quan <= 0.1
;
```
