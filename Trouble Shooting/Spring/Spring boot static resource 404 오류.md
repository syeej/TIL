## Spring boot static resource 404 오류

### 상황

![image](https://github.com/user-attachments/assets/e415be87-b93e-4bac-9949-e45b1c3a4eff)

### 원인

![image](https://github.com/user-attachments/assets/1e1ce777-66e4-4edc-bc05-8bbe80cbeaa6)

```java
@SpringBootApplication(scanBasePackages = "com.example.day0709")
public class StudySpringBootApplication {
    ...
}
```
컴포넌트 스캔 대상 패키지 지정이 올바르지 않음 

### 해결
```java
@SpringBootApplication(scanBasePackages = "com.example")
public class StudySpringBootApplication {
    ...
}
```
