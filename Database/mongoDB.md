## mongoDB

- 문서지향 저장소를 제공하는 [NoSQL](https://github.com/Soujiro-a/TIL/blob/main/Database/NoSQL.md) 데이터베이스
- 데이터를 Document, Document의 집합을 Collection(RDBMS에서는 Table)이라 칭함
- BSON(Binary JSON)형태로 각 Document가 저장됨
- 배열과 같은 기존 RDBMS에서 지원하지 않는 형태로도 저장 가능

### 특징

- Join이 없기 때문에, 원하는 방식에 맞춘 데이터 구조화가 필요
- 다양한 종류의 쿼리문을 지원
- 관리가 편함
- 스키마가 없는 데이터베이스이기 때문에 빠르게 개발하고, 필드를 추가/삭제하는게 매우 쉬움
- 수평 확장성이 용이
- 인덱싱을 제공

### vs SQL

| mySQL 용어  |     mongoDB 용어      |
| :---------: | :-------------------: |
|  database   |       database        |
|    table    |      collection       |
|    index    |         index         |
|     row     |     JSON document     |
|   column    |      JSON field       |
|    join     | embedding and linking |
| primary key |      \_id field       |
|  group by   |      aggregation      |
