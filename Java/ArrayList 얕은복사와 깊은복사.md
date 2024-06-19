## 🤓 ArrayList 객체 복사

### 1. 얕은 복사

- 다른 객체에 원본 객체의 주소값을 복사해 할당하는 것
    - 같은 원본 객체를 참조함
    - 원본과 사본이 완벽하게 동기화됨
    - **사본 객체의 인스턴스 변수의 값을 수정하면, 원본 객체에도 영향을 끼쳐 같이 수정된다.**

```java
List<String> list1 = new ArrayList<>();
list1.add("test list1");
List<String> list2 = list1; //얕은 복사
list2.set(0, "set list2");

System.out.println(list1.get(0)); // 출력결과 : set list2
System.out.println(list2.get(0)); // 출력결과 : set list2
list2.set(0, "change");
System.out.println(list1.get(0)); // 출력결과 : change
System.out.println(list2.get(0)); // 출력결과 : change
```

### 2. 깊은 복사

- 객체의 모든 값을 새로운 메모리 공간에 복사하는 것
    - 원본 객체의 모든 값을 복사해 새로운 객체를 생성함
    - 사본 객체에 있는 값을 변경해도 원본 객체에 영향을 끼치지 않음

```java
//깊은 복사 - 생성자를 통한 깊은 복사
List<String> list3 = new ArrayList<>();
list3.add("test list3");
List<String> list4 = new ArrayList<>(list3); //생성자를 통한 깊은 복사
list4.set(0, "set list4");
System.out.println(list3.get(0)); // 출력결과 : test list3
System.out.println(list4.get(0)); // 출력결과 : set list4

//깊은 복사 - addAll()메소드 통한 깊은 복사
List<String> list5 = new ArrayList<>();
list5.addAll(list3); //addAll()메소드를 통한 깊은 복사
list5.set(0, "set list5");
System.out.println(list3.get(0)); // 출력결과 : test list3
System.out.println(list5.get(0)); // 출력결과 : set list5

```

**참고사이트**

https://chunsubyeong.tistory.com/83
