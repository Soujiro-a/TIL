## Garbage Collection

**프로그램에서 더 이상 사용하지 않는 메모리를 자동으로 정리하는 것**

### Garbage Collection의 방법

1. 트레이싱

   - 한 객체에 flag를 두고, 사이클마다 메모리 관리자가 모든 객체를 추적하여 사용중인지를 표시한 뒤, 표시되지 않은 객체를 삭제하는 단계를 통해 메모리를 해제

2. 레퍼런스 카운팅
   - 한 객체를 참조하는 변수의 수를 추적하는 방법
   - 객체를 참조하는 변수는 처음에는 특정 메모리에 대해 레퍼런스가 하나 뿐이지만, 변수의 레퍼런스가 복사될 때마다 레퍼런스 카운트가 증가함.
   - 객체를 참조하고 있던 변수의 값이 바뀌거나, 변수 스코프를 벗어나면 레퍼런스 카운트는 줄어듬.
   - 레퍼런스 카운트가 0이 되면, 그 객체와 관련한 메모리는 비워도 괜찮음.

(추후 관련 내용을 더 공부하고 추가할 예정)
