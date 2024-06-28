
# final과 static final
변수, 메소드, 클래스 등에 사용됨

## final 키워드

**1. 변수에 사용될 때**
- final 변수는 한번 초기화되면 값을 변경할 수 없음(상수로 사용됨)
- 인스턴스 변수, 클래스 변수, 지역 변수 모두 적용 가능
- `final 필드명 [=초기값];`
- final 필드의 초기값을 줄 수 있는 방법
  1. 필드 선언 시
  2. 생성자에서 초기화

```java
package studyfinal;

public class Person {
    private String name;
    private int age;
    private static final String gender = "남"; //선언시 초기화

    public Person(String name, int age){
        this.name = name;
        this.age = age;
    }
    public Person(String name, int age, String gender){
        this.name = name;
        this.age = age;
        this.gender = gender; //생성자에서 초기화
    }
    public void sayHello(){
        System.out.println("Hello, My name is " + this.name);
    }
    public void sayIntro(){
        System.out.println("I'm " + this.age + "years old.");
    }
}
```


**2. 메소드에 사용될 때**
- final 메소드는 하위 클래스에서 오버라이드할 수 없음

**3. 클래스에 사용될 때**
- final 클래스는 다른 클래스가 상속할 수 없음


## static final
- 클래스 수준의 상수로 사용됨
- 클래스 로딩 시 한번 초기화되며, 모든 인스턴스가 동일한 값을 공유함
- 불변의 값을 저장하는 필드 (예: 원주율 파이, 지구 무게 및 둘레)

**초기화 방법**

```java
static final double PI = 3.14159;
static final double EARTH_SURFACE_AREA;
```

**특징**

- 객체마다 저장할 필요 없이 공용으로 선언하여 사용하기 때문에 static 이면서 final로 선언이 됨
- static final 필드는 객체마다 저장되지 않고 클래스에만 포함됨.
- 상수 이름은 모두 대문자로 작성함. 혼합된 이름의 경우 언더바(_)로 단어 연결

```java
public class Earth {
	static final double EARTH_RADIUS = 6400;
	static final double EARTH_SURFACE_AREA;

	static {
		EARTH_SURFACE_AREA = 4 * Math.PI * EARTH_RADIUS * EARTH_RADIUS;
	}
}
```

```java
public class StudyFinal {
public static void main(String[] args) {
		System.out.println("지구의 반지름: " + Earth.EARTH_RADIUS + "km");
		System.out.println("지구의 표면적: " + Earth.EARTH_SURFACE_AREA + " km^2");
	}
}
```
