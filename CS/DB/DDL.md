## DDL(Data Definition Language)

데이터를 정의하는 언어. 테이블을 생성, 변경, 삭제함.

| 명령어 | 설명|
| --- | --- |
| CREATE | 새로운 테이블을 생성 |
| ALTER | 기존 테이블 구조 변경 |
| DROP | 테이블 삭제 |
| RENAME | 기존 테이블 이름 변경 |
| TRUNCATE | 기존 테이블 초기화 |

### 1. CREATE

- DBMS에 여러 DB를 만들 수 있고, DB 하위에 여러 테이블을 만들 수 있는 계층 구조
- 각 DB마다 접근 권한을 다르게 설정할 수 있음.

![image](https://github.com/syeej/TIL/assets/141565053/7e5062c3-bcba-4cac-ae3a-fe19824f0a82)


**데이터베이스 생성**

```sql
CREATE DATABASE [데이터베이스명]
-- 예제
CREATE DATABASE test_db;
```

**테이블 생성**

```sql
CREATE TABLE [데이터베이스이름].[테이블이름] (
	[열] [데이터타입] [제약조건],
	...
)
-- 예제
CREATE TABLE test_db.students (
  name VARCHAR(255) NOT NULL,
  age INT NOT NULL,
  address VARCHAR(255) NOT NULL
)
```

| 데이터베이스 이름 | 어떤 데이터베이스 하위에 테이블을 생성할 지 |
| --- | --- |
| 테이블 이름 | 생성하려는 테이블의 이름 |
| 열 | 열의 이름 |
| 데이터 타입 | 해당 열의 데이터 타입 (ex. 정수, 문자열, 날짜, …) |
| 제약조건 | [NOT NULL | DEFAULT | PRIMARY KEY] 등의 옵션을 줄 수 있음 |

### 데이터 타입

DBMS마다 이름이 다를 수 있으므로 사용하는 DBMS의 공식문서 확인 필요

| 데이터 타입 | 설명 |
| --- | --- |
| CHAR(size) | 고정된 길이의 문자열로 저장. 예를 들어 데이터 타입을 “CHAR(5)”로 설정할 경우 “abcde”처럼 글자수가 5개인 문자열은 저장이 가능하고, “abc”처럼 글자수가 3개인 문자열을 저장할 때에도 “CHAR(5)” 만큼의 크기를 차지함  |
| VARCHAR(size) | 가변 길이의 문자열을 저장할 수 있음. 예를 들어 데이터 타입을 “VARCHAR(5)”로 설정할 경우 글자수가 1~5개인 문자열을 저장할 수 있음. 즉, “abc”, “abcde”는 저장할 수 있지만 5자를 넘어가는 “abcdefg”는 저장할 수 없음 |
| INT | 정수형 데이터를 저장할 수 있음. (1, 2, 3, …) |
| FLOAT | 실수형 데이터를 저장할 수 있음. (1.0, 2.0, 3.123, …) |
| DATE | 날짜를 저장할 수 있음. (2023-12-01) |
| TIME | 시간을 저장할 수 있음. (08:38:27) |
| TIMESTAMP | 날짜와 시간을 저장할 수 있음. (2023-12-01 08:38:27) |
- CHAR와 VARCHAR의 차이 예시
    - CHAR(10)의 필드에 길이가 5인 문자열을 저장하면, 나머지 5자리는 공백으로 채워짐.
        
        (항상 지정된 길이만큼의 저장 공간을 사용함)
        
    - VARCHAR(10)의 필드에 길이가 5인 문자열을 저장하면, 실제로 5자리의 공간만 사용함
        
        (필요한 만큼의 공간만 사용함)
        
    
    실무에서는 DB 용량도 결국 다 돈이기 때문에 고려하여 데이터 타입 지정함
    
- DATE, TIME, TIMESTAMP : 해당 데이터가 저장, 수정되는 시기를 저장할 때 유용
    ![image](https://github.com/syeej/TIL/assets/141565053/43bfd8cc-6a12-438b-b319-f7f2d6f6b7c4)

### 2. ALTER

기존 테이블의 구조를 변경하기 위해 사용

→ 데이터가 있을 때 테이블의 구조를 변경하면 예상치 못한 이슈가 발생할 수 있으므로 신중해야함.

- 새로운 열(Column) 추가
    
    ```sql
    ALTER TABLE students ADD grade VARCHAR(20)
    ```
    ![image](https://github.com/syeej/TIL/assets/141565053/f4efd61e-c3c7-4c78-b2a6-3b64e8ee9d4b)

    

- 기존 열 이름 변경
    
    ```sql
    ALTER TABLE students RENAME COLUMN grade TO great
    ```
   ![image](https://github.com/syeej/TIL/assets/141565053/832b7b65-2982-4435-ba3b-5546a79d243c)


- 기존 열 데이터 타입 변경
    - 기존 열에 저장된 데이터가 새 데이터 타입에 맞는지 확인 필요 (맞지 않으면 에러 발생할 수 있음.)
    
    ```sql
    ALTER TABLE students MODIFY COLUMN address VARCHAR(100) 
    ```
  ![image](https://github.com/syeej/TIL/assets/141565053/a8ab8f0a-b25b-4776-b61a-c78c78d98ddb)
  

- 열 삭제
    
    ```sql
    ALTER TABLE students DROP COLUMN grade
    ```
    ![image](https://github.com/syeej/TIL/assets/141565053/7ff57d9f-c668-4c79-b150-2715c4263bcb)


### 3. DROP

테이블을 삭제할 때 사용

```sql
DROP TABLE test_db.students
```

### 4. TRUNCATE

테이블의 모든 데이터를 삭제할 때 사용. 최초 생성된 테이블 초기 상태로 만들어줌.

```sql
TRUNCATE TABLE students
```


## DROP vs TRUNCATE vs DELETE 비교하기

|  | DROP | TRUNCATE | DELETE |
| --- | --- | --- | --- |
| 종류 | DDL | DDL(일부 DML) | DML |
| COMMIT | AUTO COMMIT | AUTO COMMIT | 사용자 COMMIT |
| ROLLBACK | 불가 | 불가 | 가능 |
| 명령어 수행시 | 테이블 정의 삭제 | 테이블을 최초 생성한 초기 상태로 만들어줌 | 데이터만 삭제 |
| 로그 | 남기지 않음 | 남기지 않음 | 남김 |
| 속도 | 빠름 | 빠름 | 느림 |
