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

## Tree

Node로 이루어진 자료구조

- Tree는 하나의 루트 Node를 가짐
- 루트 Node는 0개 이상의 자식 Node를 가지고 있음
- 각 자식 Node 또한 0개 이상의 자식 Node를 가지고 있음

Node들과 Node들을 연결하는 Edge들로 우성되어 있음

- Node들이 순서에 따른 나열 가능성도 있음
- 각 Node들은 반드시 부모 Node로 연결되어있진 않음
- 각 Node는 특정 자료형에 구애받지 않음

비선형 자료구조로 계층 관계를 표현

- ex) 디렉터리 구조, 사내 조직도

### 특징

- Graph의 한 종류

  - 그러나 Cycle이 존재하진 않는 하나의 연결 그래프
  - 혹은 유방향 비순환 그래프의 한 종류로 보기도 함
    - Node 자신만을 Loop하거나, Loop Circuit을 가질 수 없음

- Node가 N개인 트리는 항상 N-1개의 Edge를 가짐
- 두개의 Node 사이에 반드시 1개의 경로만을 가짐
- 순회는 Pre-order, In-order, Post-order로 이루어짐
  - Pre-order : 전위 순회. 부모 -> 왼쪽 자식 -> 오른쪽 자식 순으로 탐색
  - In-order : 중위 순회. 왼쪽 자식 -> 부모 -> 오른쪽 자식 순으로 탐색
  - Post-order : 후위 순회. 왼쪽 자식 -> 오른쪽 자식 -> 부모 순으로 탐색
- 이진 Tree, 이진 탐색 Tree, 균형 Tree(Red-Black Tree), 이진 Heap(최대/최소 Heap)등이 있음

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

## Binary Search Tree (이진 탐색 트리)

- 좌측 자식 노드에는 더 작은 값, 우측 자식 노드에는 더 큰 값을 가지고 있음
- [LinkedList](https://github.com/Soujiro-a/TIL/blob/main/Data%20Structure/LinkedList.md) 처럼 노드 간 연결은 포인터로 나타냄
- 포인터가 2개 있고, 각각 좌측/우측 자식 노드를 가리킴

### 구현

```js
function BinarySearchTree() {
  const Node = function (key) {
    this.key = key;
    this.left = null;
    this.right = null;
  };

  let root = null;

  // 새 키를 삽입
  this.insert = function (key) {
    const newNode = new Node(key);

    if (root === null) {
      root = newNode;
    } else {
      insertNode(root, newNode);
    }
  };
  // 새 노드를 추가할 위치를 찾는 함수
  const insertNode = function (node, newNode) {
    // 새 노드의 키가 현재 노드의 키 보다 작다면 노드의 좌측 자식 노드 확인
    if (newNode.key < node.key) {
      // 좌측 자식 노드가 없다면 새 노드를 추가
      if (node.left === null) {
        node.left = newNode;
      } else {
        // 아니면 재귀호출을 통해 하위 레벨로 내려감
        insertNode(node.left, newNode);
      }
    } else {
      // 아닐 경우 우측 노드를 확인
      if (node.right === null) {
        node.right = newNode;
      } else {
        insertNode(node.right, newNode);
      }
    }
  };

  // 해당 키를 가진 노드가 존재하는지 여부를 true/false로 반환
  this.search = function (key) {
    return searchNode(root, key);
  };
  const searchNode = function (node, key) {
    if (node === null) {
      return false;
    }
    if (key < node.key) {
      return searchNode(node.left, key);
    } else if (key > node.key) {
      return searchNode(node.right, key);
    } else {
      return true;
    }
  };

  // 중위 순회(In-order) 방식으로 트리의 전체 노드를 방문
  this.inOrderTraverse = function (callback) {
    inOrderTraverseNode(root, callback);
  };
  const inOrderTraverseNode = function (node, callback) {
    // base case
    if (node !== null) {
      inOrderTraverseNode(node.left, callback);
      callback(node.key);
      inOrderTraverseNode(node.right, callback);
    }
  };

  // 전위 순회(Pre-order) 방식으로 트리의 전체 노드를 방문
  this.preOrderTraverse = function (callback) {
    preOrderTraverseNode(root, callback);
  };
  const preOrderTraverseNode = function (node, callback) {
    // base case
    if (node !== null) {
      callback(node.key);
      preOrderTraverseNode(node.left, callback);
      preOrderTraverseNode(node.right, callback);
    }
  };

  // 후위 순회(Post-order) 방식으로 트리의 전체 노드를 방문
  this.postOrderTraverse = function (callback) {
    postOrderTraverseNode(root, callback);
  };
  const postOrderTraverseNode = function (node, callback) {
    // base case
    if (node !== null) {
      postOrderTraverseNode(node.left, callback);
      postOrderTraverseNode(node.right, callback);
      callback(node.key);
    }
  };

  // 트리의 최소 값/키를 반환
  this.min = function () {
    return minNode(root);
  };
  const minNode = function (node) {
    if (node) {
      while (node && node.left !== null) {
        node = node.left;
      }
      return node.key;
    }
    return null;
  };

  // 트리의 최대 값/키를 반환
  this.max = function () {
    return maxNode(root);
  };
  const maxNode = function (node) {
    if (node) {
      while (node && node.right !== null) {
        node = node.right;
      }
      return node.key;
    }
    return null;
  };

  // 키를 삭제
  this.remove = function (key) {
    root = removeNode(root, key);
  };
  const removeNode = function (node, key) {
    if (node === null) {
      return null;
    }
    if (key < node.key) {
      node.left = removeNode(node.left, key);
      return node;
    } else if (key > node.key) {
      node.right - removeNode(node.right, key);
      return node;
    } else {
      // 자식 노드가 없는 경우
      if (node.left === null && node.right === null) {
        node = null;
        return node;
      }
      // 어느 한쪽만 자식 노드가 있는 경우
      if (node.left === null) {
        node = node.right;
        return node;
      } else if (node.right === null) {
        node = node.left;
        return node;
      }
      // 자식이 양쪽 다 있는 경우
      const aux = findMinNode(node.right); // 우측 서브트리의 최소 노드를 찾음
      node.key = aux.key; // 최소 노드 값으로 수정 (키가 교체되는거라 삭제되는 것과 같은 효과)
      // 한 트리의 동일 키를 가진 노드가 중복되어 있기 떄문에, 우측 서브트리의 최소 노드는 삭제해야함
      node.right = removeNode(node.right, aux.key);
      return node;
    }
  };
  const findMinNode = function (node) {
    if (node) {
      while (node && node.left !== null) {
        node = node.left;
      }
      return node;
    }
    return null;
  };
}
```
