## Java 컴파일 과정

- 고급 언어로 작성된 .java 파일을 기계어인 byte code(즉 .class) 파일로 변환하는 과정을 의미
- **컴파일 과정**
    1. 프로그래머가 java언어로 소스코드(.java) 작성
    2. 자바 컴파일러(Java Compiler, 일반적으로 javac)가 .java 소스 파일을 컴파일
        - 이 때 컴파일 된 파일은 byte code로 변환된 파일(.class 파일)로 JVM이 실행할 수 있는 파일.
    3. 컴파일된 바이트 코드(.class파일)를 JVM의 클래스로더(Class Loader)에 전달
    4. 클래스 로더는 동적 로딩(Dynamic Loading)을 통해 필요한 클래스를 로딩 및 링크하여 런타임 데이터 영역(Runtime Data area, 즉 JVM의 메모리)에 올림
    5. 실행엔진(Execution Engine)은 JVM 메모리에 올라온 byte code들을 명령어 단위로 하나씩 가져와서 실행함.(실행엔진은 인터프리터 혹은 JIT 컴파일러 방식으로 변경)
 
#### Java에서 byte code란?
- 자바 바이트코드(Java Bytecode)란 JVM이 실행하는 바이너리 형식의 명령어 집합
- 자바 컴파일러는 소스 코드를 바이트코드로 변환하고, JVM은 이 바이트코드를 해석하고 실행함.
