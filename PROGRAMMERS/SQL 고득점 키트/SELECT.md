# Python 개발자 찾기
> MY ANSWER
```ruby
SELECT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPER_INFOS
WHERE SKILL_1 = 'Python'
      OR SKILL_2 = 'Python'
      OR SKILL_3 = 'Python'
ORDER BY ID
;
```
> ERROR
* 처음에 SKILL_1 IN 'Python' 이런 형식으로 썼었는데, 테이블에 NULL 값이 있어서 오류가 났나 했더니 IN 함수는 기본적으로 리스트를 받기 때문에 단일 문자열인 'Python'이 입력되어 오류가 발생한 것이라고 함 
> IDEA
```ruby
SELECT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPER_INFOS
WHERE 'Python' IN (SKILL_1, SKILL_2, SKILL_3)
ORDER BY ID
;
```
이렇게 IN 함수를 바르게 사용하여 더 짧은 쿼리를 만들 수 있음
