# Basic Select : Weather Observation Station 8
https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true
> 코드
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiou].*' AND CITY REGEXP '.*[aeiou]$'
;
```
## 풀이 방법
> 정규 표현식
