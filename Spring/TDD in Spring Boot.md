# TDD in Spring Boot

## TDD(Test-Driven Development, 테스트 주도 개발)
소프트웨어 개발 방법론 중 하나로, 실제 코드 작성 전에 테스트 코드 먼저 작성하는 방식

### TDD 과정 (Red-Green-Refactor 사이클)
1. Test Code 작성 [RED]
2. Test 통과하는 최소한의 Code 작성 [Green]
3. Code Refactoring [Refactor]

### TDD 장단점
- 장점
  - 테스트를 통과한 코드만 남기 때문에 버그가 적음(리팩토링 단계르르 통해 코드 품질을 지속적으로 개선)
  - 테스트를 통해 코드의 정확성을 빠르게 확인할 수 있음
- 단점
  - 테스트 작성부터 먼저 해야하기 때문에 초기 개발 속도가 느림
  - 요구사항이 명확하지 않거나 빠르게 변경되는 프로젝트에 적용하기 어려움

### Given - When - Then
1. Given : 테스트가 실행되기 전에 준비하는 단계. 테스트할 환경이나 상태를 설정함
2. When : 실제 테스트할 동작 또는 이벤트. 테스트할 코드나 메서드를 실행함
3. Then : 테스트의 결과를 검증하는 단계 (When 단계에서 실행한 결과가 기대한 대로 나왔는지 확인)

## JUnit5
Java 단위 테스트를 지원해주는 프레임워크

### 주요 어노테이션
- @Test : 테스트 메소드임을 명시
- @BeforeEach, @AfterEach : 각 테스트 메소드 전후에 실행될 메소드 지정
- @BeforeAll, @AfterAll : 모든 테스트 메소드 전후에 한번만 실행될 메소드 지정
- @DisplayName : 테스트에 대한 사용자 정의 이름 지정
- @Disabled : 테스트 메소드나 클래스 비활성화
