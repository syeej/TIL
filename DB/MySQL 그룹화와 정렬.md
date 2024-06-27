## 그룹화

같은 값을 가진 행끼리 하나의 그룹으로 뭉치는 기능

### GROUP BY

GROUP BY절에 명시된 열은 SELECT절에도 존재해야 함

```sql
SELECT 열, 집계함수
FROM 테이블
[WHERE 필터 조건]
GROUP BY 열
```

### HAVING

GROUP BY절에 의해 생성된 그룹 중 원하는 조건에 부합하는 그룹만 조회하는 구문

```sql
SELECT 열, 집계함수
FROM 테이블
[WHERE 필터 조건]
GROUP BY 열
HAVING 그룹 필터 조건
```

- GROUP BY 연산 후 HAVING절에 의해 필터링
- 실행 순서: WHERE -> GROUP BY -> HAVING

```sql
-- 학생 수가 2명 이상인 주소만 조회하고 싶을 때
SELECT address, COUNT(*)
FROM students
GROUP BY address
HAVING COUNT(*) >= 2
```

> 결과
> 

| address | count |
| --- | --- |
| 서울특별시 | 2 |
| 경기도 | 3 |
| 전라북도 | 2 |


✨**WHERE절과 차이**

- WHERE절은 개별 행을 필터링하며, GROUP BY 이전에 실행됨
- 원본 데이터에 대한 조건을 지정함

## 정렬

### ORDER BY

특정 기준에 따라 정렬하는 구문

```sql
SELECT 열, 집계함수
FROM 테이블
[WHERE 필터 조건]
GROUP BY 열
HAVING 그룹 필터 조건
ORDER BY 열 [ASC | DESC]
```

- 실행 순서: WHERE -> GROUP BY -> HAVING -> ORDER BY
- ORDER BY 절에는 어떤 열을 기준으로 정렬할 지 명시
    - ASC: 오름차순 (기본)
    - DESC: 내림차순
