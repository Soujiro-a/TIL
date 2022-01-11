## Graph

Node와 Node를 연결하는 Edge(간선)을 하나로 모아 놓은 자료구조

- 연결되어있는 Node 간의 관계를 표현할 수 있는 자료 구조
- 여러 개의 부분 그래프로 구성될 수도 있음
- ex) 지도, 지하철 노선도 최단 경로 등

### 특징

- 네트워크 모델
- 2개 이상의 경로가 가능함
  - Node 사이에 무방향/유방향 간선을 가질 수 있음
    - 무방향 : 방향이 없음. 양방향 관계를 나타냄
    - 유방향 : 방향이 있음. 단방향 관계를 나타냄
- Node 자신만을 Loop할 뿐 아니라, 간선을 통한 Loop Circuit을 가질 수 있음
- 루트 Node 개념이 없음
  - 부모-자식 관계 개념이 없음
- Cyclic(순환) 혹은 Acyclic(비순환)을 가짐

### 탐색 알고리즘

- 너비 우선 탐색(BFS) : 정점들과 같은 레벨에 있는 Node들을 먼저 탐색하는 방식
  - [Queue](https://github.com/Soujiro-a/TIL/blob/main/Data%20Structure/Queue.md)를 활용하여 방문해야할 곳, 방문한 곳을 체크하는 방식
- 깊이 우선 탐색(DFS) : 정점의 자식들을 먼저 탐색하는 방식

  - 방문해야할 곳을 [Stack](https://github.com/Soujiro-a/TIL/blob/main/Data%20Structure/Stack.md), 방문한 곳을 [Queue](https://github.com/Soujiro-a/TIL/blob/main/Data%20Structure/Queue.md)를 사용하여 체크하는 방식

- BFS, DFS 둘 다, 시간 복잡도는 Node의 수를 V, 간선의 수를 E라고 할 때 O(V+E)

### 구현

- Dictionary 클래스는 [Dictionary](https://github.com/Soujiro-a/TIL/blob/main/Data%20Structure/Dictionary.md)에 구현 부분 참고
- Queue 클래스 사용은 [Queue](https://github.com/Soujiro-a/TIL/blob/main/Data%20Structure/Queue.md)에 구현 부분 참고

```js
function Graph() {
  const vertices = [];
  const adjList = new Dictionary();

  // 정점 추가
  this.addVertex = function (v) {
    vertices.push(v);
    adjList.set(v, []);
  };

  //간선 추가 (무방향)
  this.addEdge = function (v, w) {
    // 유방향일 경우 방향에 맞게 간선을 하나만 추가하는 코드로 변경
    adjList.get(v).push(w); // v->w 방향 간선 추가
    adjList.get(w).push(v);
  };

  // 콘솔에 그래프를 출력
  this.toString = function () {
    let s = "";
    for (let i = 0; i < vertices.length; i++) {
      s += vertices[i] + " -> ";
      const neighbors = adjList.get(vertices[i]);
      for (let j = 0; i < neighbors.length; j++) {
        s += neighbors[j] + " ";
      }
      s += "\n";
    }
    return s;
  };

  // BFS를 시작할 때 아무데도 방문하지 않았다는 색깔 표시를 하기 위한 함수
  const initializeColor = function () {
    let color = [];
    for (let i = 0; i < vertices.length; i++) {
      color[vertices[i]] = "white";
    }
    return color;
  };

  // BFS (흰색: 방문x, 회색: 방문o, 검은색: 탐색o)
  // 매개변수 : (탐색을 시작할 정점, 콜백함수)
  this.bfs = function (v, callback) {
    let color = initializeColor();
    const queue = new Queue();
    queue.enqueue(v);

    while (!queue.isEmpty()) {
      const now = queue.dequeue(); // 가장 앞의 정점을 꺼냄
      const neighbors = adjList.get(u); // 해당 정점의 인접 리스트를 가져옴
      color[now] = "grey"; // 해당 정점에 대한 방문 표시
      for (let i = 0; i < neighbors.length; i++) {
        // 정점의 인접리스트들을 순회
        const adjv = neighbors[i]; // 각 인접 정점
        if (color[adjv] === "white") {
          // 방문하지 않은 상태일 경우
          color[adjv] = "grey"; // 방문 표시
          // 해당 정점에 대해 인접 리스트들을 다시 조사해야하므로 queue에 추가
          queue.enqueue(adjv);
        }
      }
      // 위에서 해당 정점 및 인접 정점 모두 확인이 끝났으므로 탐색했음(검정)을 표시
      color[now] = "black";

      // 만약 콜백함수를 받았을 경우에 해당 정점에 대해 콜백함수를 실행
      if (callback) {
        callback(now);
      }
    }
  };

  // BFS를 사용하여 입력받은 정점부터 각 정점까지의 거리 구하기
  this.BFS = function (v) {
    let color = initializeColor();
    const queue = new Queue();
    let d = []; // 거리를 나타내는 배열
    let pred = []; // v부터 모든 정점까지의 최단 경로를 계산 하기위한 선행자
    queue.enqueue(v);

    // 그래프의 모든 정점에 대해 거리와 경로 값을 초기화
    for (let i = 0; i < vertices.length; i++) {
      d[vertices[i]] = 0;
      pred[vertices[i]] = null;
    }

    while (!queue.isEmpty()) {
      const now = queue.dequeue(); // 가장 앞의 정점을 꺼냄
      const neighbors = adjList.get(u); // 해당 정점의 인접 리스트를 가져옴
      color[now] = "grey"; // 해당 정점에 대한 방문 표시
      for (let i = 0; i < neighbors.length; i++) {
        // 정점의 인접리스트들을 순회
        const adjv = neighbors[i]; // 각 인접 정점
        if (color[adjv] === "white") {
          // 방문하지 않은 상태일 경우
          color[adjv] = "grey"; // 방문 표시
          pred[adjv] = now; // 인접 정점의 선행자를 가장 앞의 정점으로 세팅
          d[adjv] = d[now] + 1; // 인접 정점과의 거리를 1 증가
          // 해당 정점에 대해 인접 리스트들을 다시 조사해야하므로 queue에 추가
          queue.enqueue(adjv);
        }
      }
      // 위에서 해당 정점 및 인접 정점 모두 확인이 끝났으므로 탐색했음(검정)을 표시
      color[now] = "black";
    }
    return {
      distances: d,
      predecessors: pred,
    };
  };

  // DFS (흰색: 방문x, 회색: 방문o, 검은색: 탐색o)
  this.dfs = function (callback) {
    let color = initializeColor();

    for (let i = 0; i < vertices.length; i++) {
      dfsVisit(vertices[i], color, callback);
    }
  };

  const dfsVisit = function (v, color, callback) {
    color[v] = "grey";
    if (callback) {
      callback(v);
    }
    const neighbors = adjList.get(v);
    for (let i = 0; i < neighbors.length; i++) {
      const adjv = neighbors[i];
      if (color[adjv] === "white") {
        dfsVisit(adjv, color, callback);
      }
    }
    color[v] = "black";
  };
}
```

## Graph vs Tree

|              | Graph                                                   | Tree                                                                                    |
| :----------: | :------------------------------------------------------ | :-------------------------------------------------------------------------------------- |
|     정의     | Node와 Node를 연결하는 간선을 하나로 모아놓은 자료 구조 | Graph, 방향성이 있는 비순환 Graph의 한 종류                                             |
|    방향성    | 무방향, 유방향                                          | 유방향                                                                                  |
|    사이클    | 가능                                                    | 불가능                                                                                  |
|  루트 노드   | 없음                                                    | 1개만 존재                                                                              |
|  부모-자식   | 없음                                                    | 있음. top-bottom or bottom-up으로 이루어져있고, 모든 자식 Node는 1개의 부모 Node를 가짐 |
|     모델     | 네트워크 모델                                           | 계층 모델                                                                               |
|     순회     | DFS, BFS                                                | DFS, BFS안의 Pre/In/Post-order                                                          |
|  간선의 수   | Graph마다 다르고, 간선이 없을 수도 있음                 | Node가 N개라면 N-1개                                                                    |
|     경로     |                                                         | 임의의 두 Node간의 경로는 유일함                                                        |
| 예시 및 종류 | 지도, 지하철 노선도의 최단경로                          | 이진 Tree, 이진 탐색 Tree, 균형 Tree(Red-Black Tree), 이진 Heap(최대/최소 Heap)         |
