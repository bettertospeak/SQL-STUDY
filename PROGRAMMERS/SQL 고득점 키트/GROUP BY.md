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

# LV2) 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기
> MY ANSWER
```ruby
SELECT CAR_TYPE
       , COUNT(*) CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%통풍시트%'
      OR OPTIONS LIKE '%열선시트%'
      OR OPTIONS LIKE '%가죽시트%'
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE
;
```
> ERROR
* IN 연산자를 사용할 수 없었음
``` ruby
SELECT CAR_TYPE
       , COUNT(*) CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS IN ('통풍시트', '열선시트', '가죽시트')
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE
;
```
OPTIONS 컬럼에는 값이 '주차감지센서,네비게이션,열선시트' 이런 식으로 들어있었음. 저 목록이 하나의 str로 들어가있었는데, 리스트 내에 해당 요소가 포함되어있는지 확인할 수 없음. 따라서 문자열이 포함되어있는지 여부를 확인해야함.
