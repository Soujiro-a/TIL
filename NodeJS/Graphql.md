## Graphql

### 관련 개념

- Over Fetching
  - 필요 이상의 데이터를 받는 것
    ex) user에서 username만 필요하지만, email, phone number와 같이 쓰이지 않을 정보까지 함께 response로 받음
- Under Fetching
  - 필요한 데이터를 받기 위해 request를 1번 이상 보내는 것
    ex) 앱 실행시, user 데이터, notification 데이터 등 필요한 데이터들을 각각의 request를 보내서 response로 받음
