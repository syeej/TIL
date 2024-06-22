# MySQL 기초


### SQL 개념

- Structured Query Language
- 데이터베이스에서 데이터를 추가, 조회, 수정, 삭제하는 프로그래밍 언어
 
| 속성 | 설명 | 주요 명령어 |
| --- | --- | --- |
| DDL | 데이터베이스나 테이블 등을 생성, 삭제하거나 그 구조를 변경하기 위한 명령어 | CREATE, ALTER, DROP |
| DML | 데이터베이스에 저장된 데이터를 처리하거나 조회, 검색하기 위한 명령어 | INSERT, UPDATE, DELETE, SELECT 등 |
| DCL | 데이터베이스에 저장된 데이터를 관리하기 위하여 데이터의 보안성 및 무결성 등을 제어하기 위한 명령어 | GRANT, REVOKE 등 |



### SQL 기본 명령어 - DML
데이터를 조회, 삽입, 수정, 삭제하기 위한 문법

- SELECT : 데이터 조회
- INSERT : 데이터 삽입
- UPDATE : 데이서 수정
- DELETE : 데이터 삭제


### 3. SELECT 쿼리문 순서

- 문법 순서
  - SELECT
  - FROM
  - JOIN
  - ON
  - WHERE
  - GROUP BY
  - HAVING
  - ORDER BY
  - LIMIT / OFFSET
- 실행 순서
  - FROM
  - ON
  - JOIN
  - WHERE
  - GROUP BY
  - HAVING
  - SELECT
  - DISTINCT
  - ORDER BY
  - LIMIT / OFFSET

SELECT절에서 지정한 Alias는 실행 순서상 WHERE나 GROUP BY 등에서 사용 불가능
  - 다만 MySQL의 경우 GROUP BY, HAVING 절에서 사용 가능



### 데이터 추가, 조회, 수정, 삭제

- 데이터 추가

```sql
INSERT INTO <테이블이름> (컬럼이름1, 컬럼이름2, ...)
VALUES (값1, 값2, ...);

INSERT INTO students (name, age, address)
VALUES ('김이박', 40, '서울특별시');

-- bulk insert
INSERT INTO students (name, age, address)
VALUES ('학생1', 20, '경기도'), ('학생2', 22, '경기도'), ('학생3', 23, '경기도');
```

- 데이터 조회

```sql
-- 모든 컬럼 조회
SELECT * FROM <테이블이름>;

-- 특정 컬럼 조회
SELECT <컬럼이름1>, <컬럼이름2> FROM <테이블이름>;

-- 조건을 만족하는 데이터 조회 (WHERE)
SELECT <컬럼이름1>, <컬럼이름2>
FROM <테이블이름>
WHERE <조건절>;

-- 원하는 개수만큼 조회 (LIMIT)
SELECT <컬럼이름1>, <컬럼이름2>
FROM <테이블이름>
LIMIT <개수>;

-- 특정 위치에서부터 조회(OFFSET)
SELECT <컬럼이름1>, <컬럼이름2>
FROM <테이블이름>
LIMIT <개수>
OFFSET <위치>;

-- 5번재 행부터 25행까지 출력(6~25)
SELECT *
FROM ORDERS
LIMIT 20
OFFSET 5;

-- 중복없이 조회 (DISTINCT)
SELECT DISTINCT <컬럼이름> FROM <테이블이름>;
```


- 데이터 수정

```sql
UPDATE <테이블이름>
SET <수정할 컬럼이름1>=<수정할 값1>, <수정할 컬럼이름2>=<수정할 값2>, ...
WHERE <조건절>;
```

- 데이터 삭제

```sql
DELETE FROM <테이블이름>
WHERE <조건절>;

-- 여러 행 삭제
DELETE
FROM STUDENTS
WHERE AGE BETWEEN 30 AND 33;

-- 모든 행 삭제
DELETE
FROM STUDENTS;
```




### COUNT, AVG, SUM, MAX, MIN

- COUNT: 조건에 맞는 데이터 개수 반환

```sql
SELECT COUNT(<컬럼이름>)
FROM <테이블이름>
WHERE <조건절>;
```

```sql
SELECT COUNT(*)
FROM 학생
WHERE 이름='홍길동';
```

- AVG: 조건에 맞는 데이터 값들의 평균값 반환

```sql
SELECT AVG(<컬럼이름>)
FROM <테이블이름>
WHERE <조건절>;
```

```sql
SELECT AVG(age)
FROM 학생
WHERE age >= 10;
```

- SUM: 조건에 맞는 데이터 값들의 합 반환

```sql
SELECT SUM(price)
FROM 상품;
```

- MAX: 조건에 맞는 데이터 값들 중 최대값 반환

```sql
SELECT MAX(price)
FROM 상품;
```

- MIN: 조건에 맞는 데이터 값들 중 최소값 반환

```sql
SELECT MIN(price)
FROM 상품;
```

