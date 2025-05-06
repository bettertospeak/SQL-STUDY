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
      AND ((GENOTYPE & 1 > 0) OR (GENOTYPE & 4 > 0))
;
```
* 왜 GENOTYPE이 4인가?
  * 2진수로 봤을때 0001(1형질→10진수로 1), 0010(2형질→10진수로 2), 0011(3형질→10진수로 4)
  * 2진주 정수를 직접 써도 되지만 2진수를 그대로 알아듣지 못하는 경우가 많기 때문에, 10진수 정수로 쓰는 것이 직관적이고 실용적
> IDEA
* 비트 연산자를 처음 들어봄 + 처음 써봄... 이해한 내용을 정리해보자
### 비트 연산자
> 비트 단위 데이터를 다룰 때 사용되는 연산자 (논리 연산자와 다름)
* & : 대응되는 비트가 양쪽 다 1이면 1 반환 (001 & 011 = 001 반환)
* | : 대응되는 비트가 한쪽이라도 1이면 1반환 (001 | 011 = 011 반환)
* ^ : 대응되는 비트가 다르면 0, 같으면 1 (001 ^ 011 = 101 반환)
* left shift, right shift 연산 추가 (말들이 좀 다름)

# LV2) 부모의 형질을 모두 가지는 대장균 찾기
> MY ANSWER
```ruby
SELECT CHILD.ID
       , CHILD.GENOTYPE AS GENOTYPE
       , PARENT.GENOTYPE AS PARENT_GENOTYPE
FROM ECOLI_DATA CHILD
JOIN ECOLI_DATA PARENT ON CHILD.PARENT_ID = PARENT.ID
WHERE (CHILD.GENOTYPE & PARENT.GENOTYPE) = PARENT.GENOTYPE
ORDER BY CHILD.ID
;
```
> ERROR
```ruby
(CHILD.GENOTYPE & PARENT.GENOTYPE) = 1
OR (CHILD.GENOTYPE ^ PARENT.GENOTYPE) != 1
```
* 위의 조건을 WHERE에 넣으면 안되는지? → 잘못됨
  * 첫 줄은 딱 한 비트만 겹쳐야 한다는 의미로 해석됨
  * 두 번째 줄은 한 비트라도 불일치하면 제외됨 
> IDEA
```
(CHILD.GENOTYPE & PARENT.GENOTYPE) = PARENT.GENOTYPE
```
* 조건이 이렇게 되어야 하는 이유?
  * 부모 형질을 모두 포함한다면 연산 결과가 부모 형질과 같아져야 함 : 비트는 숫자 뿐만 아니라 위치에 따라 형질이 달라지기 때문에! (EX. 자식 1101 & 부모 0111 = 0101 이므로 자식이 부모의 2형질을 포함하지 않아 불일치 → 이런 식으로 해석)

# LV2) 업그레이드 된 아이템 구하기
> MY ANSWER
```ruby
SELECT I.ITEM_ID
       , I.ITEM_NAME
       , I.RARITY
FROM ITEM_INFO I
WHERE I.ITEM_ID IN (
    SELECT IT.ITEM_ID
    FROM ITEM_TREE IT
    JOIN ITEM_INFO II ON IT.PARENT_ITEM_ID = II.ITEM_ID
    WHERE II.RARITY = 'RARE'
)
ORDER BY I.ITEM_ID DESC
;
```
> IDEA
* LEFT JOIN으로 ITEM_INFO - ITEM_TREE - ITEM_INFO를 계속 이으려고 했었는데 이렇게 하면 업그레이드가 더이상 되지 않는 아이템도 출력되기는 하지만, 모두 NULL처리가 되고 ITEM_ID를 기준으로 정렬하면 NULL이 가장 작은 수로 분류되어 밑으로 감

# LV2) 조건에 맞는 개발자 찾기
> MY ANSWER
```ruby
SELECT d.ID, d.EMAIL, d.FIRST_NAME, d.LAST_NAME
FROM DEVELOPERS d
WHERE d.SKILL_CODE & (
  SELECT SUM(s.CODE)
  FROM SKILLCODES s
  WHERE s.NAME IN ('Python', 'C#')
)
ORDER BY d.ID;
```
> IDEA
* 제발 테이블 이름 좀 제대로 읽기... 쿼리 잘 써놓고 테이블명 틀려서 통과가 안됨 ㅠ
