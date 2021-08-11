## EC2(Elastic Compute Cloud)

**AWS에서 원격 제어할 수 있는 가상 컴퓨터를 한 대 빌리는 것**

### 장점

1. 구성하는데 필요한 시간이 짧음
2. 다양한 운영체제에 대한 선택이 가능함
   - AMI를 통해서 운영체제 뿐만 아니라, CPU, RAM, 저장용량까지도 쉽게 구성이 가능함
   - AMI(Amazon Machine Image) : 소프트웨어 구성이 기재된 템플릿
     - 여러 템플릿이 있으며, 필요에 따라 직접 구성할 수도 있음

### Instance

- AWS에서 빌리는 1대의 컴퓨터 단위를 일컬음
  => Instance를 생성한다고 표현함.
- 자신이 선택한 AMI를 토대로 구성됨.
- **EC2 -> AMI -> Instance**
