## Relational DataBase - 관계형 데이터베이스

- 데이터의 규격인 스키마(테이블)와 각종 제약 조건을 정하고, 그에 맞게 데이터를 저장
- 대부분의 경우 SQL(Structured Query Language)로 상호작용

### 용어

row : 각 데이터 항목을 저장. record라고도 부름
column : 항목의 명칭을 나타냄. 각 항목마다 데이터 유형을 정할 수 있음. attribute, field라고도 부름
table : column의 묶음을 나타냄. column의 제약 사항을 정할 수 있음. schema라고도 부름.
Primary Key : 각 row를 구별하기위한 요소

### ORM - Object-Relational Mapping

데이터베이스의 table을 객체의 형태로 매핑하여 다룸

- SQL Query를 다루는 것보다는 직관적으로 다룰 수 있음
- 데이터베이스와의 상호작용을 한번 더 추상화 할 수 있음
  => 비교적 더 익숙한 프로그래밍 언어에서의 생산성을 높일 수 있음
