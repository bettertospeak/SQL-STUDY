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
> 이거 말고 더 간결하게 쓸 수는 없을까?
