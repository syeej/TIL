## Stream API

Java8에 도입되어 데이터를 함수형 프로그래밍 스타일로 처리할 수 있는 기능 제공

Stream은 데이터의 흐름을 나타내며, 중간 연산과 최종 연산을 통해 데이터 처리 가능

Stream은 **원본 데이터를 변경하지 않음**


### 1. Stream 생성 방법

- 컬렉션에서 Stream 생성
- 배열에서 Stream 생성
- 직접 Stream 생성

### 2. 중간 연산

Stream을 변환하고 필터링하는 등의 작업을 수행하며, **최종 연산이 호출될 때까지 실행되지 않음**

- filter() : 조건에 맞는 요소만 포함하는 새로운 Stream 생성
- map() : 각 요소에 주어진 함수를 적용한 결과로 이루어진 새로운 Stream 생성
- sorted() : 요소를 정렬한 새로운 Stream 생성

### 3. 최종 연산

Stream을 소비하여 결과를 생성하며, **최종 연산이 호출되면 Stream이 닫히며, 더 이상 사용할 수 없음**

- forEach() : Stream의 각 요소에 주어진 동작을 수행
- collect() : Stream의 요소를 수집하여 컬렉션이나 다른 형태로 변환
- reduce() : Stream의 요소를 결합하여 하나의 값으로 만듦

```java
package StudyLambda0620;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;
import java.util.stream.Stream;

public class Main0620 {
    public static void main(String[] args){
        //컬렉션에서 Stream 생성
        //List<Integer> list1 = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
        //Stream<Integer> numbers1 = list1.stream();
        //numbers1.filter(x->x%2==0); //중간연산자 : filter(), map(), sorted() <- 최종연산을 해야 함
        List<Integer> numbers1 = new ArrayList<>(Arrays.asList(1,2,3,4,5,6,7,8,9,10));
        numbers1.stream().filter(x->x%2==0);//중간연산(filter)
        System.out.println(numbers1);
        numbers1.stream().filter(n->n%2==0).forEach(n->System.out.print(n+" "));

        System.out.println();
        //배열에서 Stream 생성
        int[] arr = {1,2, 3, 4, 5, 6, 7, 8, 9, 10};
        IntStream numbers2 = Arrays.stream(arr);
        //numbers2.map(x->x*2);
        //에러 발생 : Exception in thread "main" java.lang.IllegalStateException: stream has already been operated upon or closed
        //System.out.println(numbers2);
        numbers2.map(x->x*2).forEach(x -> System.out.print(x + " "));

        System.out.println();
        //직접 Stream 생성
        Stream<Integer> intStream = Stream.of(1, 9, 2, 8, 10, 3, 7 ,4, 6, 5);
        intStream.sorted().forEach(x -> System.out.print(x + " "));

        System.out.println();
        List<Integer> list = new ArrayList<>(Arrays.asList(1,2,3,4,5,6,7,8,9,10));
        List<Integer> newList = list.stream().filter(x->x%2!=0).sorted().collect(Collectors.toList());
        System.out.println(newList);

        List<Integer> list2 = new ArrayList<>(Arrays.asList(1,2,3,4,5,6,7,8,9,10));
        int sum1 = list2.stream().reduce(0, (a, b)-> a+b);
        int sum2 = list2.stream().reduce(10, (a, b)-> a+b);
        System.out.println("SUM1 : "+sum1);
        System.out.println("SUM2 : "+sum2);

        //예제1: 홀수 필터링
        List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
        List<Integer> result = numbers.stream().filter(x->x%2!=0).collect(Collectors.toList());
        System.out.println("예제1 : " + result);

        //예제2 : 문자열 길이 매핑
        List<String> words = Arrays.asList("Java", "Stream", "API", "Example");
        List<Integer> wordsLength = words.stream().map(x->x.length()).collect(Collectors.toList());
        //List<Integer> wordsLength = words.stream().map(String::length).collect(Collectors.toList());
        System.out.println("예제2 : " + wordsLength);

        //예제3 : 단어 수 세기
        String sentence = "Java Stream API Example";
        Long count = Arrays.stream(sentence.split(" ")).count();
        System.out.println("단어 수 : " + count);
        
        //문제1. 문자열 리스트에서 길이가 홀수인 문자열만 필터링하여 출력하는 프로그램을 람다 표현식을 사용하여 작성
        List<String> wordsList = Arrays.asList("apple", "banana", "cat", "dog", "elephant", "blueberry");
        System.out.print("문제1 : ");
        wordsList.stream().filter(x-> x.length()%2!=0).forEach(x->System.out.print(x+" "));
        System.out.println();

        //문제2. 문자열 리스트에서 길이가 5 이하인 문자열만 출력하는 프로그램을 람다 표현식을 사용하여 작성하세요.
        List<String> wordsList2 = Arrays.asList("apple", "banana", "cat", "dog", "elephant", "blueberry");
        System.out.print("문제2 : ");
        wordsList2.stream().filter(x -> x.length() <= 5).forEach(x -> System.out.print(x+" "));
        System.out.println();
    }
}
```

**실행 결과**

![image](https://github.com/syeej/TIL/assets/141565053/02ea6c71-e221-4996-b35b-fa97ad9c9ccc)
