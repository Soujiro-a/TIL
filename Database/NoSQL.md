## NoSQL

스키마 없이 데이터를 표현하는 것이 주된 특징인 일련의 데이터베이스

### 특징

- 정해진 스키마가 없음
- 데이터베이스의 종류에 따라 특성이 매우 다름

#### 장점

- 높은 수평 확장성

```
수직 확장 vs 수평 확장

- 수직 확장(vertical scaling)
  - 한 인스턴스의 가용 자원(CPU, memory, storage)을 더 키워 큰 로드를 감당함
  - 어디까지나 하나의 인스턴스를 키우는 것이기 때문에 확장이 제한적임

- 수평 확장(horizontal scaling)
  - 더 많은 인스턴스를 만들어 더 큰 로드를 감당함
  - 수평 확장이 가능한 구조이고, 비용을 감당할 수 있다면 이론적으로 받아낼 수 있는 로드는 무한에 가까움
```

- 초기 개발의 용이성
- 스키마 설계의 유연성

#### 단점

- 표준의 부재
- SQL에 비해 약한 query capability
- data consistency를 어플리케이션 레벨에서 보장해야 함
  => Migration 작업을 프로그래머가 직접 관리해줘야 함

### 종류

- Key-Value
  - Redis, AWS DynamoDB
  - 모든 레코드는 key-value 페어
  - value는 어떤 값이든 될 수 있음
  - NoSQL 데이터베이스의 가장 단순한 형태
- Document-based
  - AWS DynamoDB, CouchDB, MongoDB
  - 각 레코드가 하나의 문서가 됨
  - 문서는 데이터베이스에 따라 XML, YAML, JSON, BSON 등을 사용
  - 문서의 내부적 구조를 통한 쿼리 최적화, 활용성 높은 API 제공
- Graph-based
  - Neo4j, AWS Neptune
  - 그래프 이론을 바탕으로, 데이터베이스를 그래프로 표현
  - 그래프는 node(객체)와 edge(관계), 그리고 property(객체의 속성)로 이루어짐
  - 관계가 first-class citizen(일급 객체)이기 때문에, 관계 기반 문제(실시간 추천 등)에 유리함
