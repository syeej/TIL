## 🤢 Spring Boot MySQL 연동 오류

### 문제 상황
Caused by: org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment] due to: Unable to determine Dialect without JDBC metadata (please set 'jakarta.persistence.jdbc.url' for common cases or 'hibernate.dialect' when a custom Dialect implementation must be provided)
at org.hibernate.service.internal.AbstractServiceRegistryImpl.createService(AbstractServiceRegistryImpl.java:276) ~[hibernate-core-6.5.2.Final.jar:6.5.2.Final]


- 원인 : Spring Boot 컨테이너가 MySQL Dialect 설정을 못 찾았기 때문
### 해결 
- application.yml에 코드 추가
  
  jpa.proprerties.hibernate.dialect

```yml
spring:
  application:
    name: demo
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/test_db?useSSL=false&allowPublicKeyRetrieval=True
    username: root
    password: 
  jpa:
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQLDialect
```

### 또 에러 발생
java.lang.NullPointerException: Cannot invoke "org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(java.sql.SQLException, String)" because the return value of "org.hibernate.resource.transaction.backend.jdbc.internal.JdbcIsolationDelegate.sqlExceptionHelper()" is null

### 해결 
- 데이터베이스 서버 실행으로 해결됨 mysql.server start
