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
> 수정 답
