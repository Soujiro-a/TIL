## Spanning Tree (신장 트리)

- 그래프의 모든 노드가 연결되어 있으면서 트리의 속성을 만족하는 그래프
- 신장 트리의 조건
  - 본래 그래프의 모든 노드를 포함해야 함
  - 모든 노드가 서로 연결
  - 사이클이 존재하지 않음

### 최소 신장 트리

- 그래프를 통해 만들 수 있는 신장 트리 중, 간선 가중치의 합이 최소인 신장 트리
- 최소 신장 트리를 찾는 알고리즘은 대표적으로 2가지
  - Kruskal's Algorithm
  - Prim's Algorithm

### Kruskal's Algorithm

- 모든 정점을 독립적인 집합으로 만듬(초기화)
- 모든 간선을 가중치를 기준으로 정렬하고, 비용이 작은 간선부터 양 끝의 두 정점을 비교
- 두 정점의 최상위 정점을 확인 후, 서로 다를 경우 두 정점을 연결(사이클이 생기지 않도록 하기 위함)
- [Union-Find](https://github.com/Soujiro-a/TIL/blob/main/Algorithm/Union-Find.md) 알고리즘 사용
- 시간 복잡도
  - 초기화 : O(V)
    - V : 정점의 갯수
  - 가중치 기반 간선 정렬 : O(E log E)
    - 퀵 소트를 사용할 경우에 해당
    - E : 간선의 갯수
  - 사이클이 생기지 않도록 정점 연결 : O(E)
    - 모든 간선을 검사 : O(E)
    - [Union-Find](https://github.com/Soujiro-a/TIL/blob/main/Algorithm/Union-Find.md) 알고리즘을 사용
      - union-by-rank
      - path compression
    - 위의 두 기법을 사용했을 때의 시간 복잡도 : O(M log\* N)
      - log\* N = log(log(log...(log n)))
      - 만약, N의 값이 2^65536 이더라도, log\* N = 5
      - 결과적으로, 거의 O(1), 상수 값에 가까움
  - O(V) + O(E log E) + O(E) = O(E log E)

### Prim's Algorithm

- 시작 정점을 선택 후, 정점에 인접한 간선 중 최소 간선으로 연결된 정점을 선택
- 그 후, 해당 정점에서 다시 최소 간선으로 연결된 정점을 선택하는 방식으로 최소 신장 트리를 구함
- 시간 복잡도 : O(E log E)
  - 모든 간선에 대한 검사 (최악의 경우) : O(E)
  - 최소 힙 구조 : O(log E)

#### 개선된 버전

- 간선이 아닌 노드를 중심으로 우선순위 큐를 적용하는 방식
- 로직
  - 정점:key 구조를 만들어놓고, 특정 정점의 key값은 0, 나머지 정점들의 key값은 무한대로 놓은 뒤, 모든 정점:key 값은 우선순위 큐에 넣음
  - 가장 key값이 적은 정점:key를 추출한 후, 해당 정점의 인접 정점들에 대해 key값과 간선의 가중치 값을 비교하여 간선의 가중치가 더 작으면 해장 정점:key 값을 갱신
    - 정점:key 값 갱신 시, 우선순위 큐는 최소 key값을 가지는 정점:key 를 루트노드로 올려놓도록 재구성
- 고려사항
  - 우선순위 큐 구조에서, 이미 들어가있는 데이터의 값 변경 시, 최소값을 가지는 데이터를 루트노드로 올려놓도록 재구성하는 기능이 필요
- 시간 복잡도 : O(E log V)
  - E : 간선의 갯수
  - V : 노드의 갯수

#### Kruskal vs Prim

- 공통점
  - [탐욕 알고리즘](https://github.com/Soujiro-a/TIL/blob/main/Algorithm/Greddy.md)을 기반으로 하고 있음
- 차이점
  - Kruskal : 간선의 가중치가 작은 간선부터 선택하는 방식으로 최소 신장 트리를 구함
  - Prim : 특정 정점부터, 해당 정점에 연결된 간선들 중 가중치가 작은 간선을 선택하고, 선택한 간선으로 연결된 정점들에 연결된 간선 중에서 가중치가 작은 간선을 선택하는 방식으로 최소 신장 트리를 구함
