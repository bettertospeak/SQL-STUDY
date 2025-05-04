# LV1) Python 개발자 찾기
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

# LV1) 특정 형질을 가지는 대장균 찾기
> MY ANSWER
```ruby
SELECT COUNT(ID) AS COUNT
FROM ECOLI_DATA
WHERE (GENOTYPE & 2) = 0
      AND ((GENOTYPE & 1 > 0) OR (GENOTYPE & 3 > 0))
;
```
> IDEA
* 비트 연산자를 처음 들어봄 + 처음 써봄... 이해한 내용을 정리해보자
### 비트 연산자
> 비트 단위 데이터를 다룰 때 사용되는 연산자 (논리 연산자와 다름)
* & : 대응되는 비트가 양쪽 다 1이면 1 반환 (001 & 011 = 001 반환)
* | : 대응되는 비트가 한쪽이라도 1이면 1반환 (001 | 011 = 011 반환)
* ^ : 대응되는 비트가 다르면 0, 같으면 1 (001 ^ 011 = 101 반환)
* left shift, right shift 연산 추가 (말들이 좀 다름)


