## 🤢 중복 Bean Name 오류 해결

![image](https://github.com/syeej/TIL/assets/141565053/77d4b6e6-446f-465f-a6ba-044ebc02686d)

### 발생 원인


> 💡 Caused by: org.springframework.context.annotation.ConflictingBeanDefinitionException: Annotation-specified bean name 'userRepository' for bean class [com.example.demo.studylayer.UserRepository] conflicts with existing, non-compatible bean definition of same name and class [com.example.demo.UserRepository]


@Repository가 붙은 UserRepository가 2개 있었음

### 해결

`//@Repository` 주석 처리

![image](https://github.com/syeej/TIL/assets/141565053/a5850d39-0faa-420b-859c-8ab5394359d7)
