## Primitive Type과 Reference Type
### 1. Primitive Type(원시 타입, 기본형)
- Java에서 제공되는 기본 테이터 타입이며, **각 타입마다 고정된 크기를 가짐(각 타입별 기본값 있음)**
  - 정수형 : byte(1바이트), short(2바이트), int(4바이트), long(8바이트)
  - 실수형 : float(4바이트), double(8바이트)
  - 문자형 : char(2바이트)
  - 논리형 : boolean(1바이트)
- **Stack 메모리**에 직접 값을 저장하며, Reference Type에 비해 속도가 빠름


### 2. Reference Type(참조 타입)
- 클래스, 인터페이스, 배열 등 사용자 정의 타입(기본값은 null임, 아무 객체도 참조하지 않는다는 의미)
  - String, Array, Interface
- 데이터의 실제 값이 아니라 **데이터가 저장된 메모리 주소를 참조하는 방식**
- **Heap 메모리**를 사용하고 참조를 통해 데이터에 접근하므로 Primitive Type보다 상대적으로 속도가 느림
  - Heap 메모리에 저장된 객체는 더 이상 참조되지 않으면 **Java의 Garbage Collector에 의해 자동으로 정리**됨
- 참조 변수 자체의 크기는 고정되어 있지만 실제 데이터 크기는 가변적
