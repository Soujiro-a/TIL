## HashTable

- Key-Value를 1:1로 연관지어 저장하는 자료구조(연관배열 구조)
- Key를 이용하여 Value를 도출함

### 기능

- Key, Value가 주어졌을 때, 두 값을 저장함
- Key가 주어졌을 때, 해당 Key에 연관된 Value 조회
- 기존 Key에 새로운 Value가 주어졌을 때, 기존 Value를 새로운 Value로 대체
- Key가 주어졌을 때, 해당 Key에 연관된 Value제거

### 구조

- Key
  - 고유한 값을 가짐
  - 저장 공간의 효율성을 위해 Hash Function에 입력해서 Hash로 변경 후 저장함
    - Key의 길이가 정해지지 않았기 때문에, 그대로 저장한다면 여러 길이의 저장소 구성이 필요해짐
- Hash Function
  - Key를 Hash로 바꿔주는 역할
  - 서로 다른 Key가 같은 Hash가 되는 경우(Hash 충돌)가 발생할 확률을 최대한 줄이는 함수를 만드는 것이 중요함
- Hash
  - Hash Function의 결과물로, 저장소(Bucket, Slot)에서 Value와 매칭되어 저장
- Value
  - 저장소에 최종적으로 저장되는 값
  - Key와 매칭되어 저장, 접근, 검색, 삭제가 가능함

### 동작 과정

1. Key -> Hash Function -> Hash
2. Hash를 배열의 Index로 사용함
3. 해당 Index에 Value를 저장함
   \*HashTable의 크기가 5라면, A라는 Key의 Value를 찾을 때 Hash Function("A") % 5 연산을 통해 Index 값을 계산하여 Value를 조회

### Hash 충돌

- 서로 다른 Key가 같은 Hash가 되는 경우
- Hash 충돌이 늘어날 수록 탐색의 시간 복잡도가 O(n)으로 수렴함
  - 충돌이 없을 때에는 O(1)에 가까움

#### 해결 방법

1. Separating Chaining
   - Java Development Kit 내부에서 사용하는 충돌 처리 방식을 말함
   - Linked List(데이터 6개 이하) 또는 Red-Black Tree(데이터 8개 이상) 사용
   - Linked List 사용 중 충돌이 발생하면, 충돌이 발생한 Index가 가리키고 있는 Linked List에 Node를 추가하여 Value를 삽입
   - Key에 대한 Value 탐색, 삭제 시에는 인덱스가 기리키고 있는 Linked List를 선형 검색을 통해 Value를 반환
   - Linked List 구조 덕분에 추가 데이터 수에 대한 제약이 적은 편
2. Open addressing
   - 추가 메모리 공간을 사용하지 않고, HashTable 배열의 빈 공간을 사용하는 방법
   - Separating Chaining에 비해 메모리 사용이 적음
   - 방법은 Linear Probing, Quadratic Probing, Double Hashing 등이 있다고 함
3. Resizing
   - 저장 공간이 일정 수준에 도달했을 경우에 Resizing을 함
     - Separating Chaining의 경우에는 성능 향상이 목적
     - Open addressing의 경우 배열 크기 확장이 목적
   - 확장 임계점은 현재 데이터 개수가 Hash Bucket 개수의 75%가 될 때

### 장점

- 적은 리소스로 많은 데이터를 효율적으로 관리할 수 있음
  - 하드디스크, 클라우드에 있는 많은 데이터를 Hash로 매핑하여 작은 크기의 메모리로 프로세스 관리가 가능
- 배열의 Index를 사용하기 때문에 검색뿐만 아니라 삽입, 삭제를 빠르게 할 수 있음
  - Index는 데이터의 고유 위치이기 때문에, 삽입, 삭제시 다른 데이터를 이동할 필요가 없어서 빠른 속도로 가능
- Key와 Hash에 연관성이 없어서 보안상 유리함
- 데이터 캐싱에 많이 사용함
  - GET, PUT 기능에 캐시 로직 추가 시 자주 사용하는 데이터 바로 검색 가능
- 중복을 제거하는데 유용함

### 단점

- Hash 충돌의 가능성
- 공간 복잡도가 증가함
- 순서를 따르지 않음
- 해시 함수에 의존적

### HashTable vs HashMap

#### 공통점

- Key-Value 구조 및 Key에 대한 Hash로 Value를 관리하는 부분

#### 차이점

- HashTable
  - 동기
  - Key-Value 값으로 null을 허용하지 않음
    - Key가 hashcode(), equals()를 사용하기 때문
  - 보조 Hash Function과 separation Chaining을 사용해서 비교적 충돌이 덜 발생함
- HashMap
  - 비동기
  - Key-Value 값으로 null 허용
