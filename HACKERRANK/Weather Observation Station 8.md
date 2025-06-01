# Basic Select : Weather Observation Station 8
https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true
> 코드 1번
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiou].*' AND CITY REGEXP '.*[aeiou]$'
;
```
> 코드 2번
```ruby
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiou].*[aeiou]$'
;
```
## 풀이 방법 : 정규 표현식
```
WHERE CITY REGEXP '^[aeiou].*[aeiou]$'
```
* ^ : 시작
* [abc] : abc 중 하나
* . : 문자
* .* : 문자의 반복 = 문자열
* $ : 끝
