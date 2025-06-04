# 1. 고객별 총 구매금액 구하기
* 고객별로 결제 완료된(PAID) 주문의 총 금액을 구하라.
* 결과는 고객 이름과 총금액을 출력하되, 총금액이 높은 순으로 정렬하라.

  -- Customers
+----+----------+
| id | name     |
+----+----------+
| 1  | Alice    |
| 2  | Bob      |
| 3  | Charlie  |
+----+----------+

-- Orders
+----+------------+---------+--------+
| id | customer_id| amount  | status |
+----+------------+---------+--------+
| 1  | 1          | 100     | 'PAID' |
| 2  | 2          | 200     | 'CANCELLED' |
| 3  | 1          | 150     | 'PAID' |
| 4  | 3          | 300     | 'PAID' |
+----+------------+---------+--------+

> 최초 답
```ruby
SELECT C.NAME, SUM(O.AMOUNT)
FROM CUSTOMERS C
LEFT JOIN ORDERS O ON C.ID = O.ID
WHERE STATUS IS ‘PAID’
ORDER BY SUM(O.AMOUNT) DESC
;
```
> 수정 답
