# DCL(Data Control Language)

### 사용 목적

1. DB 접근 권한 관리
2. **Transaction 관리** (Transaction : 트랜잭션, 하나의 기능을 수행하기 위한 하나의 논리적인 작업 단위)
    - 트랜잭션 예시 - 은행 송금 시스템
        
         A가 B에게 10,000원을 송금한다고 했을 때 내부적으로 아래와 같은 과정을 거친다고 가정
        
        1. A의 계좌 -10,000원
        2. B의 계좌 +10,000원
        
        1번 작업이 실패하면 2번 작업은 의미가 없음. 1번이 실패하면 2번은 무조건 실패 처리
        
        1-2번 작업은 하나의 트랜잭션 (논리적으로 하나의 작업)
        

### **트랜잭션 속성 : ACID**

- Atomicity 원자성
    
    트랜잭션에 속한 각각의 문(CRUD)을 하나의 단위로 취급
    
- Consistency 일관성
    
    트랜잭션이 테이블에 변경 사항을 적용할 때 미리 정의된, 예측된 방식만 취하며, 트랜잭션 일관성이 확보되면 데이터 무결성이 보장됨.
    
- Isolation 격리성
    
    여러 사용자가 같은 테이블에서 모두 동시에 CRUD 작업을 할 때, 각각의 트랜잭션을 격리하면 동시 트랜잭션이 발생해도 마치 하나씩 발생하는 것처럼 발생할 수 있음
    
- Durability 영속성
    
    트랜잭션 실행으로 인해 데이터에 적용된 변경 사항이 저장되도록 보장함.(시스템 오류가 발생해도 동일)
    

### 주요 DCL

| GRANT | 권한 부여 |
| --- | --- |
| REVOKE | 권한 박탈 |
| COMMIT | 트랜잭션 적용 |
| ROLLBACK | 트랜잭션 취소, 복구 |

### COMMIT, ROLLBACK

트랜잭션을 관리하기 위해 사용

COMMIT / ROLLBACK / AUTO COMMIT

1. Table 생성 후 데이터 생성 (create table은 auto commit 명령어임)
![image](https://github.com/syeej/TIL/assets/141565053/4c977bc8-efbf-46e5-b64b-016ab6ff91e7)

2. COMMIT 하지 않으면 다른 세션에서 볼 수 없음
![image](https://github.com/syeej/TIL/assets/141565053/90f0be73-6e83-4c66-9dd6-4a78dea21fc5)

3. COMMIT
![image](https://github.com/syeej/TIL/assets/141565053/1dc0076a-dbc8-45f3-a9e6-2239417d568b)

4. COMMIT 후라 다른 세션에서 볼 수 있음.
![image](https://github.com/syeej/TIL/assets/141565053/3d42a76a-207f-4751-bf03-a23a405bb609)



## ROLLBACK 테스트

1. INSERT 되돌리기 실습
![image](https://github.com/syeej/TIL/assets/141565053/51d609e3-7d7a-4c9d-bd92-f204b921e466)

2. ROLLBACK
![image](https://github.com/syeej/TIL/assets/141565053/e5270168-bf9f-49b8-8637-badb7c17ddee)


- **이미 커밋이 된 트랜잭션은 롤백할 수 없음**
    
    커밋 또는 롤백을 안 할 경우 디스크에 반영 안 된 상태로 메모리에 남아있음.
    
![image](https://github.com/syeej/TIL/assets/141565053/b909c029-d860-46c1-b340-8e858205732f)

![image](https://github.com/syeej/TIL/assets/141565053/19404e24-164a-4b6c-9dbd-a5a3982a5876)


### REVOKE, GRANT

접근 권한 관리 명령어, 데이터베이스 관리자가 주로 관리함

**REVOKE**

```sql
REVOKE [권한] ON [테이블명] FROM [권한을 박탈할 사용자]
```

**GRANT**

```sql
GRANT [권한] ON [테이블명] TO [권한을 받을 사용자]
```

**관리되는 권한 종류**

| SELECT | 조회 권한 |
| --- | --- |
| UPDATE | 수정 권한 |
| INSERT | 삽입 권한 |
| DELETE | 삭제 권한 |
| ALL | 모든 권한 |
