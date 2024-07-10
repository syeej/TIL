# Spring DI
## 의존성 주입(DI, Dependency Injection)
객체 간의 의존성을 외부에서 주입하는 디자인 패턴

예시 - Car 클래스는 Engine 클래스에 의존하고 있는 상황
```java
public interface Engine {

}
```
```java
public class Car {
    private Engine engine;

    // Car클래스가 Engine객체를 직접 생성하지 않고, 생성자를 통해 외부(파라미터)에서 주입받음.
    public Car(Engine engine) { 
        this.engine = engine;
    }
}
```
### @Autowired
- 스프링 컨테이너에게 해당 객체의 의존성을 자동으로 주입하는데 사용되는 어노테이션
- @Autowired 어노테이션을 사용하면 객체 간의 의존성을 스프링 컨테이너가 자동으로 관리해주면서 코드의 가독성과 유지보수성 향상됨
- 주로 생성자, 필드, 메소드에 사용됨

```java
public interface MyInterface {
    void doSomething();
}
```

```java
@Component
public class B1 implements MyInterface {
    @Override
    public void doSomething() {
        System.out.println("B1 is doing something");
    }
}
```

```java
@Component
public class B2 implements MyInterface {
    @Override
    public void doSomething() {
        System.out.println("B2 is doing something");
    }
}
```

```java
@Component
public class B {
    private final MyInterface myInterface;

    @Autowired
    public B(MyInterface myInterface) {
        this.myInterface = myInterface;
    }

    public void executeTask() {
        myInterface.doSomething();
    }
}
```

### @Qualifier
- @Autowired 어노테이션과 함께 사용되어 주입할 빈을 구체적으로 지정할 때 사용됨
- 동일한 타입의 빈이 여러 개 있을 때 @Autowired는 주입할 빈을 결정할 수 없지만 @Qualifier는 어떤 빈을 주입할 지 명시적으로 지정 가능

```java
@Component
public class UserService {
    @Autowired
    @Qualifier("userRepositoryImpl")
    private UserRepository userRepository;
    
    // ...
}
```

## Spring에서 DI 방법(3가지)
1. Setter 주입 방법
2. field 주입 방법
3. **생성자 주입 방법 ← Spring 공식문서에서 권장되는 방식**

### 1. Setter 주입 방법

- setter() 메소드에 `@Autowired` 어노테이션을 붙여 의존성을 주입받음
- 장점
    - 의존성이 선택적일 때 사용할 수 있음
    - 의존성을 나중에 변경할 수 있는 유연성을 제공
- 단점
    - 의존성 주입이 객체 생성 이후에 이루어지므로, 의존성이 주입되지 않은 상태로 객체가 사용될 수 있음
    - 세터 메서드를 public으로 노출해야 하므로 캡슐화가 약화될 수 있음

```java
@Service
public class MyService {
    private MyDependency myDependency;

    @Autowired
    public void setMyDependency(MyDependency myDependency) {
        this.myDependency = myDependency;
    }

    // ...
}
```

### 2. field 주입 방법

- 클래스의 필드에 `@Autowired` 어노테이션을 붙여 의존성을 주입하는 방법
- 장점
    - 코드가 간결해짐
    - 의존성 주입을 위한 별도의 코드(생성자나 세터 메서드)가 필요하지 않음
- 단점
    - 의존성을 변경하기 어려워 유연성이 낮음
    - 의존성이 명시적으로 표현되지 않아 코드의 가독성이 떨어질 수 있음

```java
@Service
public class MyService {
    @Autowired
    private MyDependency myDependency;

    // ...
}
```

**@Primary**

이름이 같은 Bean이 여러 개일 때 우선순위


**@Qualifier**

Bean이 여러 개일 때 대상 명시

### 3. 생성자 주입 방법 - ⭐ 권장되는 방법 ⭐

- 클래스의 생성자를 통해 의존성을 주입하는 방법
- 생성자의 매개변수로 의존성을 받아들이고, 주입받은 의존성을 클래스 내부에서 사용함
- 장점
    - 의존성이 필수적이므로 객체 생성 시점에 의존성이 주입되지 않으면 컴파일 에러 발생.
    - 불변성(Immutability)을 유지할 수 있음 → 한번 의존성이 주입되면 변경하지 못함(`final` 키워드)
    - 의존성이 명확하게 표현되어 코드의 가독성이 좋음
- 단점
    - 의존성이 많아지면 생성자의 매개변수가 많아져 코드의 복잡성이 증가할 수 있음

```java
@Service
public class MyService {
    private final MyDependency myDependency;

    @Autowired
    public MyService(MyDependency myDependency) {
        this.myDependency = myDependency;
    }

    // ...
}
```

문제점 : 의존성이 많아질수록 생성자가 길어짐

```java
@Service
public class MyService {
    private Test1 test1;
    private Test2 test2;
    private Test3 test3;
    
    public MyService(Test1 test1, Test2 test2, Test3 test3){
	    this.test1 = test1;
	    this.test2 = test2;
	    this.test3 = test3;
    }

    public String hello() {
        System.out.println(this.helper);
        return "Hello, Spring Boot!";
    }
}
```

해결 : `@RequiredArgsConstructor`를 통해 final 필드가 포함된 생성자를 만들어줌

```java
@Service
@RequiredArgsConstructor
public class MyService {

    private final Helper helper;
    private final Test1 test1;
    private final Test2 test2;
    private final Test3 test3;

    public String hello() {
        System.out.println(this.helper);
        return "Hello, Spring Boot!";
    }
}
```

### 왜 생성자 주입 방식을 권장할까?
- 객체의 불변성
  - final 키워드에 의해 인스턴스가 생성될 때 한번만 할당되며 값을 변경할 수 없어서 객체의 불변성이 보장됨 
- 순환 참조 문제 예방
  - 순환 참조란 두 객체가 각각 서로 필드에 포함하여 참조하고 있는 상태.(서로의 객체를 계속 생성하는 무한반복 상태에 빠지게됨)
  - setter 주입, field 주입은 runtime 에러 발생하여 서비스 진행 중 문제를 야기할 수 있지만 생성자 주입은 컴파일 타임에 에러가 발생하여 미리 예방 가능
- 초기에 할당되기 때문에 Null Pointer Exception이 발생하지 않음
