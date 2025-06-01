# Basic Select : Weather Observation Station 9
https://www.hackerrank.com/challenges/weather-observation-station-9/problem?isFullScreen=true
> 풀이 코드
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiouAEIOU]'
;
```
* 주의사항 : 도시 이름은 대문자로 시작하는 경우가 있어서, 대소문자 함께 조회
> 다른 코드
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE LOWER(CITY) REGEXP '^[^aeiou]'
;
```
* CITY를 소문자로 바꿔서 정규표현식에 대입

## 성능은 LOWER을 쓰지 않는 쪽이 나음
변환 때문에 CPU 연산 추가됨
