# LV2) 진료과 별 총 예약 횟수 출력하기
> MY ANSWER
```ruby
SELECT MCDP_CD AS '진료과코드'
       , COUNT(*) AS '5월예약건수'
FROM APPOINTMENT
WHERE APNT_YMD LIKE '2022-05%'
GROUP BY MCDP_CD
ORDER BY COUNT(*), MCDP_CD
;
```
> ERROR
```ruby
SELECT MCDP_CD AS '진료과코드'
       , COUNT(*) AS '5월예약건수'
FROM APPOINTMENT
WHERE APNT_YMD LIKE '2022-05%'
GROUP BY MCDP_CD
ORDER BY '5월예약건수', '진료과코드'
;
```
* 실행 안된 이유 : ORDER BY절에 SELECT의 ALIAS를 사용했기 때문
