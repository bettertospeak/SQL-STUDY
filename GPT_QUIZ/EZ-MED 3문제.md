# 1. 고객별 총 구매금액 구하기
* 고객별로 결제 완료된(PAID) 주문의 총 금액을 구하라.
* 결과는 고객 이름과 총금액을 출력하되, 총금액이 높은 순으로 정렬하라.
<img width="390" alt="Image" src="https://github.com/user-attachments/assets/106113d7-66b5-4c02-8bfc-d268357e923d" />
> 최초 답
```ruby
SELECT C.NAME, SUM(O.AMOUNT)
FROM CUSTOMERS C
LEFT JOIN ORDERS O ON C.ID = O.ID
WHERE STATUS IS ‘PAID’
ORDER BY SUM(O.AMOUNT) DESC
;
```
> 수정할 부분
1. JOIN 조건 오류 : CUSTOMERS는 회원 아이디, ORDERS는 주문 아이디이므로,\
  * C.ID = O.ID 가 아니라 C.ID = O.CUSTOMER_ID로 조인해줘야 함
2. 집계함수를 쓸때는 sort_values 조건을 GROUP BY절에 써줘야함
> 수정 답
```ruby
SELECT C.NAME, SUM(O.AMOUNT) AS TOTAL_AMOUNT
FROM CUSTOMERS C
LEFT JOIN ORDERS O ON C.ID = O.CUSTOMER_ID AND O.STATUS = 'PAID'
GROUP BY C.NAME
ORDER BY TOTAL_AMOUNT DESC
;
```
---
# 2. 월별 신규 가입자 수 구하기
* 각 월(예: 2023-01, 2023-02, ...)별 신규 가입자 수를 구하라.
* 결과는 월별 오름차순으로 정렬하라.
<img width="412" alt="Image" src="https://github.com/user-attachments/assets/81dcd6b1-ef8d-4067-8b84-f8855ceaae9e" />
> 최초 답
```ruby
SELECT MONTH(SIGNUP_DATE) AS MONTHS, COUNT(*)
FROM USERS
GROUP BY MONTHS
ORDER BY MONTHS
;
```
> 수정할 부분
1. MONTH로만 집계하면 2023-01과 2024-01이 같은 월로 집계되므로, YYYY-mm 형식으로 추출해줘야 함
2. 집계함수를 쓸때는 sort_values 조건을 GROUP BY절에 써줘야함
> 수정 답
```ruby
SELECT DATE_FORMAT(SIGNUP_DATE, '%Y-%m') AS SIGNUP_DATE
       , COUNT(*) AS SIGNUP_COUNT
FROM USERS
GROUP BY SIGNUP_DATE
ORDER BY SIGNUP_DATE
;
```
