## Spring Framework

Java Application 개발을 위한 오픈 소스 프레임워크

### 장점

1. **의존성 주입(DI, Dependency Injection)** : Spring은 객체 간의 의존성을 관리해주는 기능을 함
2. **관점 지향 프로그래밍(AOP, Aspect-Oriented Programming)** : 공통적인 기능을 한 곳에서 관리할 수 있게 해줌
3. 다양한 모듈 제공
4. 테스트 용이성

### 단점

1. 복잡성 : 다양한 기능으로 인해 프로젝트가 커지고 복잡해질 수 있음 (설계의 중요성)
2. 런타임 오버헤드 : 내부적으로 많은 일을 처리하므로, 약간의 속도 저하가 발생할 수 있음

### Spring과 Spring Boot의 차이

Spring과 Spring Boot 모두 Spring  Framework 기반 도구이지만 Spring Boot는 개발자가 별도 설정 파일을 작성할 필요 없이, 프로젝트 설정과 라이브러리 의존성을 자동으로 처리해주는 기능을 제공함.

또한 내장된 서버(Tomcat, Jetty 등)를 제공하여 별도의 서버 설정 없이 애플리케이션을 실행할 수 있음

Spring은 자세하게 제어하고 싶을 때, Spring Boot는 빠르고 간단하게 개발하고자 할 때 사용됨.
