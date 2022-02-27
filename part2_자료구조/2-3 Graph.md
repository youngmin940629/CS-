# Graph

### 정점과 간선의 집합 => Graph

트리 또한 그래프이며, 그 중 사이클이 허용되지 않는 그래프를 말함.

### 그래프 관련 용어 정리

#### Undirected Graph 와 Directed Graph (Digraph)

말 그대로 정점과 간선의 연결관계에 있어서 방향성이 없는 그래프를 Undirected Graph 라고 하고, 간선에 방향성이 포함되어 있는 그래프를 Directed Graph라고 한다.

- Directed Graph (Digraph)

```
V = {1, 2, 3, 4, 5, 6}
E = {(1, 4), (2,1), (3, 4), (3, 4), (5, 6)}
(u, v) = vertex u에서 vertex v로 가는 edge
```

- Undirected Graph

```
V = {1, 2, 3, 4, 5, 6}
E = {(1, 4), (2,1), (3, 4), (3, 4), (5, 6)}
(u, v) = vertex u와 vertex v를 연결하는 edge
```

#### Degree

Undirected Graph에서 각 정점에 연결된 Edge의 개수를 Degree라고 한다. 

Directed Graph에서 간선에 방향성이 존재하기 때문에 Degree 가 두 개로 나뉘게 된다. 간선의 개수를 Outdegree라 하고, 들어오는 간서의 개수를 Indegree라 함



#### 가중치 그래프(Weight Graph)와 부분 그래프(Sub Graph)

가중치 그래프란 간선에 가중치 정보를 두어 구성한 그래프를 말함.

비가중치 그래프는 모든 간선의 가중치가 동일한 그래프.

부분 집합과 유사한 개념으로 부분그래프라는것이 있는데 이는 본래의 그래프의 일부 정점 및 간선으로 이루어진 그래프를 말하는것.



#### 그래프를 구현하는 두 방법

- 인접 행렬 (adjacent matrix) : 정방 행렬을 사용하는 방법
  - 해당하는 위치의 value값을 통해서 정점 간의 연결 관계를 O(1)으로 파악할 수 있다. Edge 개수와는 무관하게 V^2의 Space Complexity를 갖는다. Dense graph를 표현할 때 적절한 방법이다.
- 인접 리스트 (adjacent list) : 연결 리스트를 사용하는 방법
  - 정점의 인접 리스트를 확인해봐야 하므로 정점간 연결되어 있는지 확인하는데 오래걸림. Space Complexity는 O(E+V)이다. Sparse graph를 표현하는데 적당한 방법이다.





#### 그래프 탐색

- 깊이 우선 탐색 (Depth First Search : DFS)
  - 그래프 상에 존재하는 임의의 한 정점으로부터 연결되어 있는 한 정점으로만 나아간다라는 방법을 우선으로 탐색
  - 연결할 수 있는 정점이 있을 때까지 계속 연결하다가 더 이상 연결되지 않은 정점이 없으면 그 전 단계의 정점으로 돌아가 연결할 정점이 있는지 살펴봄.
  - 즉, 미로찾기처럼 구성하면 되는것인데 Stack 자료구조에서 사용한다.
  - Time Complexity : O(V+E) ... 정점 개수 + Edge 개수
- 너비 우선 탐색 (Breadth First Search : BFS)
  - 그래프 상에 존재하는 임의의 한 정점으로부터 연결되어 있는 모든 정점으로 나아감
  - Queue를 사용한다.
  - 탐색을 시작하는 정점을 Queue에 넣는 enqueue. 그리고 dequeue를 하면서 정점과 간선으로 연결되어 있는 정점들을 enqueue한다. 즉, 방문 순서대로 queue에 저장하는 방법
  - Time Complexity : O(V+E) ... 정점 개수 + edge 개수 => BFS 로 구한 경로는 최단경로이다.



#### Minimum Spanning Tree

그래프 G의 spanning tree 중 edge weight 의 합이 최소인 `spanning tree`를 말한다. 여기서 말하는 `spanning tree`란 그래프 G의 모든 정점이 cycle 없이 연결된 형태를 말함

- Kruskal Algorithm
  - 초기화 작업으로 __edge 없이__ 정점들만으로 그래프를 구성. 
  - weight가 제일 작은 edge부터 검토. 그러기 위해 Edge set을 non-decreasing 으로 sorting 해야함
  - 가장 작은 weight에 해당하는 edge를 추가하는데 추가할 때 그래프에 cycle이 생기지 않는 경우에만 추가함
  - spanning tree가 완성되면 모든 정점들이 연결된 상태로 종료가 되고 완성될 수 없는 그래프에 대해서는 모든 edge에 대해 판단이 이루어지면 종료됨!
  -  [Kruskal Algorithm의 세부 동작과정](https://gmlwjd9405.github.io/2018/08/29/algorithm-kruskal-mst.html) [Kruskal Algorithm 관련 Code](https://github.com/morecreativa/Algorithm_Practice/blob/master/Kruskal Algorithm.cpp)

- 어떻게 cycle 생성 여부를 판단하는가?
  - Graph의 각 정점에 `set-id`라는 것을 추가적으로 부여. 그리고 초기화 과정에서 모두 1~n 까지의 값으로 각각 정점들을 초기화 한다. 여기서 0은 어떠한 edge와도 연결되지 않았음을 의미하게 된다. 그리고 연결할 때마다 `set-id`를 하나로 통일 시키는데, 값이 동일한 `set-id` 개수가 많은 `set-id`값으로 통일시킨다.
- Time Complexity
  - Edge의 weight를 기준으로 sorting - O(E log E)
  - cycle 생성 여부를 검사하고 set-id를 통일 - O(E + V log V ) => 전체 시간 복잡도 : O(E log E)

#### Prim Algorithm

초기화 과정에서 한 개의 정점으로 이루어진 초기 그래프 A를 구성. 그리고 나서 그래프 A 내부에 있는 정점으로 부터 외부에 있는 정점 사이의 edge를 연결하는데 그 중 가장 작은 weight의 edge를 통해 연결되는 정점을 추가한다. 어떤 정점이건 간에 상관없이 edge의 weight를 기준으로 연결하는 것.

이렇게 연결된 정점은 그래프 A에 포함된다. 위 과정을 반복하고 모든 정점들이 연결되면 종료

- Time Complexity => O(E log V)