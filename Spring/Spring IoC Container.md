## Spring IoC Conainer


### IoC
- Inversion of Control의 약자로, 제어의 역전을 의미
- 객체의 생성 및 생명주기에 대한 **모든 객체에 대한 제어권이 바뀌었다는 것**을 의미함

```java
public class A {
  B b = new B();  // 클래스 A 에서 필요한 B 객체를, new 키워드를 사용하여 생성
}
```
#### 스프링 컨테이너가 객체를 관리하는 방식
```java
interface B{}
```
```java
public class B1 implements B{}

```
```java
public class B2 implements B{}
```
```java
public class A {
  private B b;
  // 코드에서 객체를 생성하지 않고, 어디선가 받아온 객체를 b에 할당 (B 인터페이스를 구현한 B1, B2 모두 가능)
  public A(B b){
    this.b = b;
  }
}
```

### Spring IoC Container(= Spring Conatiner)
- Spring Container는 객체(Bean)을 생성하고 관리하는 역할 ( 빈의 모든 생명주기를 스프링 컨테이너가 관리함)
- 개발자가 @Autowired 혹은 생성자를 사용하여 빈을 주입할 수 있게 DI를 지원함
- 개발자가 어떤 객체를 요청하면 컨테이너에서 그 객체를 제공해주는 행위

  (제어를 개발자가 아닌 컨테이너(Spring)가 하면서 제어가 역전됨)
- IoC 컨테이너를 사용하면 객체 간의 결합도를 낮추고, 코드 재사용성과 개발 생산성을 높일 수 있음

#### BeanFactory
- Bean을 등록, 수정 등 관리하고 의존관계를 설정(DI를 처리)하는 기능을 담당하는 가장 기본적인 IoC 컨테이너인 인터페이스
- 일반적으로 BeanFactory를 바로 사용하지 않고, 이를 확장한 ApplicationContext를 사용

#### ApplicationContext
- 해당 Application에 대한 구상정보를 제공하는 인터페이스
- Bean을 관리하는 기능은 BeanFactory와 같지만 Spring의 부가 기능을 추가로 제공하여 BeanFactory보다 권장

