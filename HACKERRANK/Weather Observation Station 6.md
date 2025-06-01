# Basic Select : Weather Observation Station 6
https://www.hackerrank.com/challenges/weather-observation-station-6/problem?isFullScreen=true
> 내가 써서 통과된 코드
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE 'a%'
      OR CITY LIKE 'e%'
      OR CITY LIKE 'i%'
      OR CITY LIKE 'o%'
      OR CITY LIKE 'u%'
;
```
# Basic Select : Weather Observation Station 7
https://www.hackerrank.com/challenges/weather-observation-station-7/problem?isFullScreen=true
> 내가 써서 통과된 코드
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '%a'
      OR CITY LIKE '%e'
      OR CITY LIKE '%i'
      OR CITY LIKE '%o'
      OR CITY LIKE '%u'
;
```
> 두 코드 다 간결하게 쓰는 방법 없을까?
> 6번 정규표현식
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiouAEIOU]'
;
```
> 7번 정규표현식
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[aeiou]$'
;
```
