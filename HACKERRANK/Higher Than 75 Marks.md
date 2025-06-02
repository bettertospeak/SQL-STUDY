# Basic Select : Higher Than 75 Marks
https://www.hackerrank.com/challenges/more-than-75-marks/problem?isFullScreen=true
```ruby
SELECT NAME
FROM STUDENTS
WHERE MARKS > 75
ORDER BY SUBSTR(NAME FROM -3), ID
;
```
## 문자열 추출, SUBSTR/SUBSTRING
```
SUBSTR('HELLO' FROM 1)
SUBSTR('HELLO', 1)
```
* 'HELLO'의 1번째부터 끝까지 추출
```
SUBSTR('HELLO' FROM 2 FOR 2)
SUBSTR('HELLO', 2, 2)
```
* 'HELLO'의 2번째 문자부터 2개 추출
