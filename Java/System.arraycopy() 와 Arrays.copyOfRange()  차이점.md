### System.arraycopy() 와 Arrays.copyOfRange()  차이점

두 메소드 모두 배열의 데이터를 복하는 역할을 하지만 **사용 방식과 결과물이 다름**

1. **System.arraycopy(Object arr, int startIdx, Object target, int targetIdx, int length)**
    - 원본 배열(arr)의 startIdx부터 length만큼의 데이터를 대상 배열(target)의 targetIdx부터 복사
    - 대상 배열에 원본 배열의 데이터를 덮어씀
    - 원본 배열과 대상 배열의 타입이 같아야함
    - 사용 예시
        
        ```java
        int[] arr = {1, 2, 3, 4, 5};
        int[] target = new int[10];
        
        // arr 배열의 인덱스 1부터 3개의 요소를 target 배열의 인덱스 4부터 복사
        System.arraycopy(arr, 1, target, 4, 3);
        
        // target 배열의 결과: [0, 0, 0, 0, 2, 3, 4, 0, 0, 0]
        ```
        
2. **Arrays.copyOfRange(Object arr, int start , int end)**
    - 원본 배열(arr)의  start 인덱스부터 end인덱스 전까지 데이터를 새로운 배열에 복사하여 반환함
        
        (원본 배열의 타입과 동일한 타입의 새로운 배열)
        
    - 사용 예시
        
        ```java
        int[] arr= {1, 2, 3, 4, 5};
        
        // arr 배열의 인덱스 1부터 4 전까지의 요소를 새로운 배열에 복사
        int[] newArr = Arrays.copyOfRange(arr, 1, 4);
        
        // newArr 배열의 결과: [2, 3, 4]
        ```
        

💫**주요  차이점** 

`System.arraycopy()`는 기존 배열에 데이터를 덮어쓰지만, `Arrays.copyOfRange()`는 새로운 배열을 생성함. 

일반적으로 `System.arraycopy()`는 성능상의 이점이 있지만, 배열의 길이를 변경할 수 없기 때문에 `Arrays.copyOfRange()`가 더 유연할 수 있음
