
# Python3

코딩테스트에 자주 사용되는 문법 정리


## 자료형

### 정수형

```python
#양의 정수
a = 1000
print(a)

#음의 정수
b = -7
print(b)

#0
c = 0
print(c)
```

### 실수형

- 소수점 아래의 데이터를 포함하는 수 자료형
- 파이썬에서는 변수에 소수점을 붙인 수를 대입하면 실수형 변수로 처리됨
    
    소수부가 0이거나, 정수부가 0인 소수는 0을 생략하고 작성할 수 있음
    

```python
# 두 실수형 변수 선언
x = 5.5
y = 2.0

# 실수형 연산
sum_result = x + y
difference_result = x - y
product_result = x * y
quotient_result = x / y

# 결과 출력
print("x+y:", sum_result)            # 덧셈  7.5
print("x-y:", difference_result)  # 뺄셈 3.5
print("x*y:", product_result)        # 곱셈 11.0
print("x/y:", quotient_result)      # 나눗셈 2.75
print("x//y:", x//y)  # 2.0

# 실수형과 정수형 변수 선언
float_num = 7.5
int_num = 2

# 실수형과 정수형 간의 연산
sum_result = float_num + int_num
difference_result = float_num - int_num
product_result = float_num * int_num
quotient_result = float_num / int_num

# 결과 출력
print("Sum:", sum_result)            # 덧셈  9.5
print("Difference:", difference_result)  # 뺄셈 5.5
print("Product:", product_result)        # 곱셈 15.0
print("Quotient:", quotient_result)      # 나눗셈 3.75
```

### 수 자료형의 연산

- 파이썬은 나누기 연산자(/) 사용 시 나눠진 결과를 **실수형으로 반환함**
- 몫을 얻기 위해 몫 연산자(//)를 사용

```python
result = 7 / 2
print(result)  # 출력: 3.5

result = 7 // 2
print(result)  # 출력: 3
```

- 거듭제곱 연산자 (**)

```python
# 2의 3제곱을 계산
result = 2 ** 3
print(result)  # 출력: 8

# 10의 2제곱을 계산
result = 10 ** 2
print(result)  # 출력: 100

# 3의 0.5제곱 (즉, 제곱근)을 계산
result = 3 ** 0.5
print(result)  # 출력: 1.7320508075688772
```

## 리스트 자료형

- 배열(Array)의 기능 및 연결 리스트와 유사한 기능 제공
- 리스트 대신에 배열 혹은 테이블이라고도 부름

### 리스트 초기화

- 리스트는 대괄호`[]` 안에 원소를 넣어 초기화하며, 쉼표`,` 로 원소를 구분함
- 비어있는 리스트를 선언하고자 할 때는 `list()` 혹은 간단히 `[]`를 이용할 수 있음
- 리스트의 원소에 접근할 때는 인덱스(index) 값을 괄호에 넣음 **(0부터 시작함)**

```python
#직접 데이터 넣어서 초기화
a = [1,2,3,4,5,6,7,8,9]
print(a)

#5번째 원소 출력
print(a[4])

#크기가 n이고, 모든 값이 0인 1차원 리스트 초기화
n = 10
arr=[0]*10
print(arr)
```

### 리스트의 인덱싱과 슬라이싱

- 인덱싱(Indexing) : 인덱스 값을 입력하여 리스트의 특정 원소에 접근하는 것
    - 파이썬은 인덱스 값을 양의 정수와 음의 정수 모두 사용할 수 있음
        
        (음의 정수일 경우, 원소를 거꾸로 탐색하게 됨)
        
    
    ```python
    # 리스트 인덱싱
    a = [1,2,3,4,5,6,7,8,9]
    # 8번째 원소 출력
    print(a[7]) #8
    # 뒤에서 첫 번째 원소 출력
    print(a[-1]) #9
    # 뒤에서 3번째 원소 출력
    print(a[-3]) #7
    # 8번째 원소 변경
    a[7] = 10 
    print(a[7]) #10
    ```
    
- 슬라이싱(Slicing) : 연속적인 위치를 갖는 원소들을 가져와야 할 때
    - 대괄호 안에 콜론 `:` 을 넣어서 시작 인덱스와 끝 인덱스를 설정할 수 있음 (시작인덱스≤   <끝 인덱스)
    
    ```python
    a = [1,2,3,4,5,6,7,8,9]
    # 슬라이싱
    print(a[1:4]) # [2, 3, 4]
    ```
    

### **리스트 컴프리헨션**

- 리스트를 초기화 하는 방법 중 하나
- 대괄호 안에 조건문과 반복문을 적용하여 리스트를 초기화할 수 있음

```python
# 0부터 9까지의 수를 포함하는 리스트
arr = [i for i in range(10)]
print(arr) # [1,2,3,4,5,6,7,8,9]

# 0부터 19까지 수 중에서 홀수만 포함하는 리스트
arr1 = [i for i in range(20) if i%2 ==1]
print(arr1) #[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]

# 1부터 9까지의 수들의 제곱 값을 포함하는 리스트
arr2 = [i*i for i in range(1, 10)]
print(arr2) # [1, 4, 9, 16, 25, 36, 49, 64, 81]
```

- 2차원 리스트를 초기화할 때 효과적으로 사용 될 수 있음
    - 특히 N x M 크기의 2차원 리스트를 한번에 초기화 해야할 때 유용
    
    ```python
    # NxM 크기의 2차원 리스트를 초기화할 때 
    n = 4
    m = 3
    array = [[0]*m for _ in range(n)]
    print(array) # [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]]
    
    # 잘못된 예시
    # array = [[0]*m]*n
    # 전체 리스트 안에 포함된 각 리스트가 모두 같은 객체로 인식됨
    ```
    

**언더바(_)** 

- 반복을 수행하되 반복을 위한 변수의 값을 무시하고자 할 때 언더바 `_` 를 자주 사용

```python
# 사용 예시
for _ in range(5):
    print("Hello")
```

### 자주 사용하는 리스트 메서드

| 함수명 | 사용법 | 설명 | 시간 복잡도 |
| --- | --- | --- | --- |
| append() | 변수명.append() | 리스트에 원소 하나 삽입할 때 사용 | O(1) |
| sort() | 변수명.sort() | 오름차순 정렬 | O(NlogN) |
| sort() | 변수명.sort(reverse=True) | 내림차순 정렬 | O(N) |
| reverse() | 변수명.reverse() | 리스트의 원소 순서를 모두 뒤집음 | O(N) |
| insert() | insert(삽입할 위치 인덱스, 삽입할 값) | 특정 인덱스 위치에 원소 삽입 | O(N) |
| count() | 변수명.count(특정 값) | 리스트에서 특정 값을 가진 데이터의 개수 | O(N) |
| remove() | 변수명.remove(특정 값) | 특정 값을 갖는 원소를 제거하는데, 여러 개일 경우 하나만 제거함 | O(N) |

```python
b = [3, 2, 4, 1]
print(b) # [3, 2, 4, 1]
b.append(4)
print(b) # [3, 2, 4, 1, 4]
b.sort()
print(b) # [1, 2, 3, 4, 4]
b.sort(reverse=True)
print(b) #[4, 4, 3, 2, 1]
b.reverse()
print(b) # [1, 2, 3, 4, 4]
b.insert(3, 9) 
print(b) #[4, 4, 3, 9, 2, 1]
print(b.count(4)) # 2
b.remove(4)
print(b) #[1, 2, 3, 9, 4]
```

- 리스트에서 특정 값을 가지는 원소 모두 제거하기

```python
c = [1,2,3,4,4,4,6]
remove_set = {3, 4} # 집합 자료형
#remove_set에 포함되어 있지 않은 값들만 result에 반환
result = [i for i in c if i not in remove_set]
print(result) #[1, 2, 6]
```

## 문자열 자료형

- 문자열 변수를 초기화하는 법 : 큰따옴표(”)나 작은 따옴표(’) 이용
    - 문자열 안에 큰 따옴표(”) 혹은 작은 따옴표(’)가 포함되어야 하는 경우
        - 전체(큰 따옴표) - 내부(작은 따옴표)
        - 전체(작은 따옴표) - 내부(큰 따옴표)
        - 백슬래시(\)를 사용하면, 큰 따옴표나 작은 따옴표를 원하는 만큼 포함시킬 수 있음

```python
word = 'Hello Python'
print(word) #Hello Python

word = 'Hello \"Python\"'
print(word) #Hello "Python"
```

### 문자열 연산

- 변수에 덧셈(+)을 이용하면 문자열이 더해져서 연결됨
    
    (문자열 변수를 양의정수와 곱하는 경우, 그만큼 여러번 더해짐)
    
- 문자열에 대해서 인덱싱(indexing)과 슬라이싱(slicing)을 이용할 수 있지만 **특정 인덱스의 값을 변경할 수 없음(Immutable)**

```python
word = 'Hello Python'
print(word[1:3]) #el

word = 'Hello \"Python\"'
print(word*3) #Hello "Python"Hello "Python"Hello "Python"
```

## 튜플 자료형

- 리스트와 유사하지만 **튜플은 한번 선언된 값을 변경할 수 없음.**
- 튜플은 소괄호`()`를 이용함
- 리스트에 비해 상대적으로 공간 효율적임

```python
ex = (1,2,3,4,5,6,7,8,9)
print(ex[4]) #5
print(ex[1:5]) #(2, 3, 4, 5)
ex[3] = 0 #TypeError: 'tuple' object does not support item assignment
```

### 튜플을 사용하면 좋은 경우(in 코테)

- 서로 다른 성질의 데이터를 묶어서 관리해야할 때
    - 최단 경로 알고리즘(비용, 노트 번호)의 형태로 튜플 자료형을 자주 사용
- 데이터의 나열을 해싱(Hashing)의 키 값으로 사용해야 할 때
    - 튜플은 변경이 불가능하므로 키값으로 사용될 수 있음(리스트는 키값으로 사용 불가)
- 리스트보다 메모리를 효율적으로 사용해야 할때

## 사전 자료형

- 키(Key)와 값(Value)의 쌍을 데이터로 가지는 자료형
- 키와 값의 쌍을 데이터로 가지며, 변경 불가능(imutable) 자료형을 키로 사용할 수 있음
- 해시 테이블(Hash Table)을 이용하므로 데이터의 조회 및 수정에 있어서 O(1)의 시간에 처리할 수 있음.

```python
data = dict()
data['사과'] = 'apple'
data['바나나'] = 'banana'
print(data) #{'사과': 'apple', '바나나': 'banana'}

if '사과' in data:
    print("'사과'를 키로 갖는 데이터 있음") #'사과'를 키로 갖는 데이터 있음

# 사전 자료형 초기화
d = {
    '홍길동' : 80,
    '고길동' : 79
}
print(d) #{'홍길동': 80, '고길동': 79}
```

### 사전 자료형 메소드

- 키와 값을 별도로 뽑아내기 위한 메소드
    - keys() : 키 데이터만 뽑아서 리스트로 이용할 때
    - values() :  값 데이터만 뽑아서 리스트로 이용할 때

```python
key_list = data.keys()
print(key_list) #dict_keys(['사과', '바나나'])
value_list = data.values()
print(value_list) #dict_values(['apple', 'banana'])

# 사전 자료형 초기화
d = {
    '홍길동' : 80,
    '고길동' : 79
}
print(d)
print(d['고길동']) #79
keys = list(d.keys())
print(keys) #['홍길동', '고길동']
```

## 집합 자료형

- 주요 특징 : **중복 허용 하지 않음, 순서 없음**
- 초기화 방법
    - 리스트 혹은 문자열을 이용해서 초기화할 수 있음 ( `set()` 함수 이용)
    - 중괄호`{}` 안에 각 원소를 콤마`,` 를 기준으로 구분하여 삽입
- 데이터 조회 및 수정에서 O(1)의 시간에 처리 가능

```python
#집합 자료형 초기화 방법1
data_set = set([1, 1, 2, 3, 3, 4, 5])
print(data_set) #{1, 2, 3, 4, 5}

#집합 자료형 초기화 방법2
data_set2 = {1,1,2,3,3,4,4,5}
print(data_set2) #{1, 2, 3, 4, 5}
```

### 집합 자료형의 연산

- 합집합 : 집합 A에 속하거나 B에 속하는 원소로 이루어진 집합
- 교집합 : 집합 A, 집합 B 둘다 속하는 원소로 이루어진 집합
- 차집합 : 집합 A의 원소 중 B에 속하지 않는 원소들로 이루어진 집합

```python
a = set([1, 3, 5, 7, 9, 10])
b = set([2,4,6,8,10])
print(a|b) #{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
print(a&b) #{10}
print(a-b) #{1, 3, 5, 7, 9}
```

### 집합 자료형 관련 함수

```python
b = set([2,4,6,8,10])
#새로운 원소 추가
b.add(3)
print(b) #{2, 3, 4, 6, 8, 10}
#새로운 원소 여러 개 추가
b.update([5,6,7])
print(b) #{2, 3, 4, 5, 6, 7, 8, 10}
#특정 값 원소 삭제
b.remove(10)
print(b) #{2, 3, 4, 5, 6, 7, 8}
```

---

## 정리

- 리스트와 튜플 : 순서가 있기 때문에 인덱싱을 통해 자료형의 값을 얻을 수 있음
- 사전과 집합 : 순서가 없기 때문에 인덱싱으로 값을 얻을 수 없음
    - 사전의 키 혹은 집합의 원소를 이용해 O(1)의 시간 복잡도로 조회
    - 키나 원소의 값으로는 변경 불가능한 문자열이나 튜플과 같은 객체가 사용되어야 함
