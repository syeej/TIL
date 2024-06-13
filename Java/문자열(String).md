

## 1. 문자열(String)이란

```java
String a = "123";
String b = "Hello World";
String c = "s";
```

- String은 Java 내장 클래스로 java.lang 패키지에 포함되어 있어 별도의 import 없이도 바로 사용 가능함.
- Java는 문자열 조작과 처리를 위해 다양한 기능(메소드)들을 제공하고 있음.
    - 내장 클래스
        - 자바 플랫폼의 핵심 패키지 java.lang.java.util. [java.io](http://java.io) 등에 포함되어 자바 실행 환경과 함께 제공되는 기본 클래스
        - 사용자가 별도로 작성하거나 외부 라이브러리에 포함된 클래스가 아닌 자바 언어 자체에 포함된 표준 클래스

## 2. 문자열 내장 메소드

### 문자열 비교 : equals

equals는 말 그대로 문자열 2개가 같은지 비교하여 결과값을 리턴

```java
String a = "hello";
String b = "java";
String c = "hello";

System.out.println(a.equals(b));
System.out.println(a.equals(c));
```

```java
false
true
```

- 문자열 a와 문자열 b에는 “hello”와 “java”가 각각 저장되어 있으므로 값이 서로 다르므로 equals 메서드를 호출하면 `false`를 리턴
- 문자열 a와 문자열 c는 “hello”와 “hello”로 값이 서로 같으므로 equals 메서드 호출 시 `true`를 리턴
- **`==` 과 `equals` 비교**
    - `==` 자료형이 같은 객체인지(같은 메모리 주소값을 갖는지) 판별
    - `equals` 문자열 값이 같은지 판별
    
    ```java
    String a = "hello";
    String b = new String("hello");
    
    System.out.println(a.equals(b));  // true
    System.out.println(a == b);  // false
    ```
    
    ```java
    true
    false
    ```
    
    문자열 a와 b는 모두 “hello”로 값이 같지만 `equals`를 호출하면 true를, `==` 연산자를 사용하면 false를 리턴합니다. **a와 b는 값은 같지만 서로 다른 객체이기 때문**입니다. `==`은 2개의 자료형이 같은 객체인지(=같은 주소값을 갖는지)를 판별할 때 사용하는 연산자이므로 false를 리턴합니다. 
    

### 특정 문자열의 위치 찾기: indexOf

indexOf는 문자열에서 `특정 문자열이 시작되는 위치(인덱스값)`를 리턴

```java
String a = "Hello World!";
System.out.println(a.indexOf("!")); // 11
```

### 특정 문자열 포함 여부: contains

contains 메서드는 문자열에서 특정 문자열이 포함되어있는지 여부를 반환 **(대소문자 구분함)**

```java
String b = "ESTSOFT";
System.out.println(b.contains("SOFT")); //true
System.out.println(b.contains("soft")); //false
```

### 특정 위치 문자 찾기: charAt

charAt 메서드는 문자열에서 특정 위치의 문자를 리턴

```java
String findchar = "What is your hobby";
System.out.println(findchar.charAt(5));
for(int i=13; i<=17; i++){
    System.out.print(String.valueOf(findchar.charAt(i)));
}
```

### 문자열 교체: replaceAll

replaceAll 메서드는 문자열에서 특정 문자열을 다른 문자열로 바꿀 때 사용

```java
String a = "Hello World!";
System.out.println(a.replaceAll("World", "Spring"));  //Hello Spring!
```

- **replace 관련 메소드 ( ✔️추가공부)**
    - replace(char oldChar, char newChar)
        - 문자열 내 지정된 oldChar 문자를 newChar 문자로 대체한 새로운 문자열을 반환
    - replace(CharSequence target, CharSequence replacement)
        - 문자열 내 지정된 target 문자열을 replacement 문자열로 대체한 새로운 문자열을 반환
    - replaceAll(String regex, String replacement)
        - 문자열 내 정규 표현식 regex와 매칭되는 모든 부분 문자열을 replacement 문자열로 대체한 새로운 문자열을 반환
    - replaceFirst(String regex, String replacement)
        - 문자열 내 정규 표현식 regex와 매칭되는 첫 번째 부분 문자열을 replacement 문자열로 대체한 새로운 문자열을 반환
    - String.valueOf(Object obj).replace(CharSequence target, CharSequence replacement)
        - 지정된 객체 obj를 문자열로 변환한 후, 문자열 내 target 부분 문자열을 replacement로 대체한 새로운 문자열을 반환
    
    ```java
    System.out.println("Hello World".replace('l', 't'));
    //Hetto Wortd
    System.out.println("Hello Worlds World".replace("World", "Java"));
    //Hello Javas Java
    System.out.println("Hello123World456".replaceAll("\\d+", "#"));
    //Hello#World#
    System.out.println("Hello123World456".replaceFirst("\\d+", "#"));
    //Hello#World456
    System.out.println(String.valueOf(123.45).replace(".", ","));
    //123,45
    ```
    

### 문자열 자르기: substring

substring 메서드는 문자열에서 특정 문자열을 뽑아낼 때 사용  **substring(시작 인덱스≤ a < 끝 인덱스)**

```java
String a = "Hello World!";
System.out.println(a.substring(3, 5));
```

```java
String a = "WEEE ASKE   :ND";
System.out.println(a.substring(0, 3) + a.substring(7, 9)+ a.substring(a.length()-2, a.length()));
//WEEKEND
```

### 대소문자 변환: toUpperCase, toLowerCase

toUpperCase 메서드는 문자열을 모두 대문자로 변경할 때 사용

toLowerCase 메서드는 문자열을 모두 소문자로 변경할 때 사용

```java
String a = "Hello World!";
System.out.println(a.toUpperCase());
```

```java
HELLO WORLD!
```

### 문자열 구분: split

split 메서드는 문자열을 특정한 구분자로 나누어 문자열 배열로 반환합니다.

```java
String a = "a:b:c:d";
String[] result = a.split(":");  // result는 {"a", "b", "c", "d"}
```

위의 예시처럼 a:b:c:d라는 문자열을 “:” 콜론으로 나누어 result에 문자열 배열로 넣을 수 있습니다. 

### 문자열 결합: concat

contcat 메서드는 문자열을 합치는 역할을 하고, 결과값은 문자열로 반환

> 문자열.**concat**(”합치고자 하는 문자열”)
> 

```java
String result = "Hello";
System.out.println(result.concat("!"));   // 결과 : Hello!
```

### String 타입의 내장 메서드

| 메서드명 | 역할 |
| --- | --- |
| equals(비교 문자열) | 두개의 문자열이 같은지 비교하여 결과를 true/false로 반환 |
| indexOf(문자) | 인자로 받은 문자가 시작되는 위치(인덱스)를 반환 |
| contains(특정 문자열) | 특정 문자열이 포함되어있는지를 true/false로 반환 |
| charAt(특정위치 인덱스) | 인자로 받은 특정 위치(인덱스)의 문자를 반환 |
| replaceAll(문자열, 문자열) | 인자로 정규식(regex)을 받아서 해당 형태로 문자열을 변경할 때 사용 |
| replace(regex, 문자열) | 문자열에서 특정 문자열을 다른 문자열로 바꿀 때 사용 |
| substring(시작인덱스, 끝인덱스) | 문자열에서 특정 문자열을 뽑아낼 때 사용 |
| toUpperCase() | 문자열을 모두 대문자로 변경할 때 사용 |
| toLowerCase() | 문자열을 모두 소문자로 변경할 때 사용 |
| split(구분자) | 문자열을 특정한 구분자로 나누어 문자열 배열로 반환 |
| concat(”합치고자 하는 문자열”) | 인자로 받은 문자열을 이전 문자열과 합쳐서 반환 |

## 3. 문자열 포맷(format)

- 가독성을 위해 2~3개 사용하는 것이 좋다.

```java
String.format("... **%s**.. **%s**..", 치환값1, 치환값2);
```

```java
String name1 = "Tim";
int age1 = 30;
String name2 = "Anna";
int age2 = 45;
System.out.println(String.format("%s의 나이는 %s세 입니다.", name1, age1));
System.out.println(String.format("%s의 나이는 %s세 입니다.", name2, age2));

System.out.println(String.format("%s의 나이는 %d세 입니다.", name1, age1));
System.out.println(String.format("%s의 나이는 %d세 입니다.", name2, age2));
```

🤔 **궁금했던 점**

- int타입이 %d가 아니라 %s여도 상관없을까?
    
    → 자바가 자동으로 int값을 String으로 변환하여 출력함**(원칙적으로 %d가 맞음)**
    
- 문자열 포맷을 사용하는 이유?
    
    코드의 가독성, 유연성, 디버깅 편의성, 성능 향상에 도움.
    

## 4. StringBuffer / StringBuilder

문자열을 추가하거나 변경할 때(연산) 주로 사용하는 자료형

String 자료형으로 +연산이나 concat() 메소드로 문자열을 이어 붙일 수 있지만, 이때 String 특성상 **새로운 객체를 생성하고 String 공간을 할당하기 때문에** 공간의 낭비 뿐만 아니라 속도면에서도 비효율적임.

⇒ 문자열 연산이 필요할 때는 `StringBuffer`혹은 `StringBuilder`를 사용

### append

- 문자열을 생성(추가)하는 메서드

```java
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append("World");
System.out.println(sb);
//String str1 = sb; //에러 String타입 필요
String str2 = sb.toString();

StringBuffer buffer = new StringBuffer();
buffer.append("hello");
buffer.append("buffer");
System.out.println(buffer);
//String str3 = buffer;  //에러 String타입 필요
String str4 = buffer.toString();
```

💡 **왜 toString()메소드를 사용하지 않아도 될까?**

`System.out.println()`의 내부 동작 방식 때문.
`System.out.println()`은 전달받은 객체의 `toString()` 메서드를 자동으로 호출하여 그 결과 문자열을 출력함.
따라서 `StringBuilder` 객체를 전달하면 내부적으로 `sb.toString()`이 호출되어 문자열로 변환된 후 출력됨.
그러나 일반적으로는 가독성과 명확성을 위해 `StringBuilder`를 `String`으로 변환할 때는 `toString()` 메서드를 명시적으로 호출하는 것이 좋음.
특히 다른 객체와의 연산이나 메서드 호출 등에서는 자동 변환이 발생하지 않을 수 있으므로 주의해야 함.


### insert

- 특정 위치에 원하는 문자열을 삽입할 수 있음.

```java
StringBuffer buffer = new StringBuffer();
buffer.append("Hello");
buffer.append("World");

System.out.println("buffer "+buffer); //"hellobuffer"
System.out.println(buffer.insert(2, "ya")); // "heyallobuffer"
System.out.println(buffer.insert(0, "C")); // "Cheyallobuffer"
System.out.println(buffer.insert(buffer.length(), " World"));
 // "Cheyallobuffer World"
```
