# Math

- Math클래스는 java.lang 패키지에 포함된 클래스로, 수학에서 자주 사용하는 상수들과 함수들을 미리 구현해 놓은 클래스
- 모든 메소드가 static method로 구현되어 있어서 따로 객체를 생성하지 않아도 사용할 수 있음.

## 코테에서 자주 사용하는 메소드

### 절대값 : Math.abs()

- 전달된 값의 절대값을 반환 (반환 타입은 double)
- 메소드
    - static double abs(double x)
    - static double abs(float x)
    - static double abs(int x)
    - static double abs(long x)
        
        ```java
        System.out.println(Math.abs(10));    // 10
        System.out.println(Math.abs(-10));   // 10
        System.out.println(Math.abs(-3.14)); // 3.14
        ```
        

### 최댓값 & 최솟값 : Math.max() & Math.min()

- max() : 전달된 두 값을 비교하여 그 중 큰 값 반환
- min() : 전달된 두 값을 비교하여 그 중 작은 값 반환
    
    ```java
    System.out.println(Math.max(3.14, 3.14159)); // 3.14159
    System.out.println(Math.min(3.14, 3.14159)); // 3.14
    System.out.println(Math.max(-10, -11));      // -10
    System.out.println(Math.min(-10, -11));      // -11
    ```
    

### 제곱 연산 : Math.pow()

- 전달된 2개의 double형 값으로 제곱 연산 수행
- pow(a, b) → a의 b승 반환
    
    ```java
    System.out.println((int)Math.pow(5, 2)); // 25
    ```
    

 

### 제곱근 : Math.sqrt()

- 전달된 double형 값의 제곱근 값 반환
    
    ```java
    System.out.println((int)Math.sqrt(25));  // 5
    ```
    

### 반올림 : Math.round()

- 전달받은 실수를 소수점 첫째 자리에서 반올림한 정수 반환
    
    ```java
    System.out.println(Math.round(10.0));     // 10
    System.out.println(Math.round(10.4));     // 10
    System.out.println(Math.round(10.5));     // 11
    ```
    

### 올림 : Math.ceil()

- 전달받은 값과 같거나 큰 수 중에서 **가장 작은 정수를** 반환
    
    ```java
    System.out.println(Math.ceil(10.0));      // 10.0
    System.out.println(Math.ceil(10.1));      // 11.0
    System.out.println(Math.ceil(10.000001)); // 11.0
    ```
    

### 내림 : Math.floor()

- 전달받은 값과 같거나 작은 수 중에서 **가장 큰 정수를** 반환
    
    ```java
    System.out.println(Math.floor(10.0));     // 10.0
    System.out.println(Math.floor(10.9));     // 10.0
    ```
    

### 난수 : Math.random()

- 0.0 이상 1.0 미만의 범위에서 임의의 double형 값을 하나 생성하여 반환
    
    ```java
    System.out.println((int)(Math.random() * 100)); // 0 ~ 99
    
    //java.util 패키지의 Random 클래스의 nextInt()메소드로 난수 생성 가능
    Random ran = new Random();
    System.out.println(ran.nextInt(100));           // 0 ~ 99
    
    System.out.println((int)(Math.random() * 6));       // 0 ~ 5
    System.out.println(((int)(Math.random() * 6) + 1)); // 1 ~ 6
    System.out.println(((int)(Math.random() * 6) + 3)); // 3 ~ 8
    ```
    

**참고사이트**

[코딩교육 티씨피스쿨](https://www.tcpschool.com/java/java_api_math)
