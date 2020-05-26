# 트리 (Tree)

---

# 트리의 개념

노드들과 노드들을 잇는 엣지들로 이루어진 자료 구조.

![https://gmlwjd9405.github.io/images/data-structure-tree/tree-terms.png](https://gmlwjd9405.github.io/images/data-structure-tree/tree-terms.png)

출처: [https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)

- 루트 노드(Root Node): 부모가 없는 노드, 트리는 하나의 루트 노드만을 가진다.
- 자식 노드(Child Node): 부모 노드와 인접한 하위 노드
- 단말 노드(Leaf Node): 자식이 없는 노드, '말단 노드' 또는 '잎 노드'라고도 한다.
- 내부 노드(Internal Node): 단말 노드가 아닌 노드
- 간선(Edge): 노드를 연결하는 선
- 형제(Siblings): 같은 부모를 가지는 노드
- 노드의 크기(size): 자신을 포함한 모든 자손 노드의 갯수
- 노드의 깊이(depth): 루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수. 높이(height)라고도 한다.
- 노드의 레벨(level): 트리의 특정 깊이를 가지는 노드의 집합
- 노드의 차수(degree): 특정 노드가 지닌 자식 노드
- 트리의 차수(degree of tree): 트리의 최대 차수
- 트리의 높이(height): 루트 노드에서 가장 깊숙히 있는 노드의 깊이

## 트리의 특징

- DAG(Directed Acyclic Graph)의 일종(그래프의 한 종류)이며, '최소 연결 트리'라고도 한다.
- 계층 모델이다.
- 트리에는 사이클(cycle)이 존재할 수 없다.
- 노드의 수 = 엣지의 수 + 1
- 트리의 순회 종류에는 Pre-order, In-order, Post-order가 있다.
- 이진 탐색(DFS, BFS), 우선순위 큐(최대 힙, 최소 힙)에 사용되는 자료구조다.

## 트리의 종류

- 이진 트리: 각 노드가 최대 두 개의 자식 노드를 갖는 트리
- 이진 탐색 트리: 노드의 갯수 n이 `모든 왼쪽 자식 노드 ≤ n < 모든 오른쪽 자식 노드`를 만족하는 트리
- 균형 트리: O(log N) 시간에 insert와 find를 할 수 있을 정도로 균형이 잘 잡혀 있는 경우

![https://gmlwjd9405.github.io/images/data-structure-tree/tree-types-example.png](https://gmlwjd9405.github.io/images/data-structure-tree/tree-types-example.png)

순서대로 전, 완전, 포화 이진 트리
출처: [https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)

- 전 이진 트리: 모든 노드가 0개 또는 2개의 자식 노드를 갖는 트리
    - 

    ![https://gmlwjd9405.github.io/images/data-structure-tree/Full-Binary-Tree.png](https://gmlwjd9405.github.io/images/data-structure-tree/Full-Binary-Tree.png)

    출처: [https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)

- 완전 이진 트리: 최하단 레벨을 제외한 모든 레벨에서 노드가 포화 상태인 이진 트리. 최하단 레벨의 노드들은 반드시 왼쪽에서부터 채워져야 한다.

    ![https://gmlwjd9405.github.io/images/data-structure-tree/Complete-Binary-Tree.png](https://gmlwjd9405.github.io/images/data-structure-tree/Complete-Binary-Tree.png)

    출처: [https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)

- 포화 이진 트리: 모든 레벨에서 노드가 포화 상태인 이진 트리. 전 이진 트리, 완전 이진 트리의 특징을 모두 만족한다.

    ![https://gmlwjd9405.github.io/images/data-structure-tree/Perfect-Binary-Tree.png](https://gmlwjd9405.github.io/images/data-structure-tree/Perfect-Binary-Tree.png)

    출처: [https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)

- 이진 힙
    - 최소 힙: 각 노드의 값이 자식 노드의 값보다 *작은 경우*를 만족하는 완전 이진 트리.
    - 최대 힙: 각 노드의 값이 자식 노드의 값보다 *큰 경우*를 만족하는 완전 이진 트리.

    [힙 (Heap)](Heap%20a8b1c5c4664d4d279ebc307c20b9c946.md)

## 사용 사례

주로 계층적 관계를 표현해야 할 때 트리를 사용한다.

- 디렉터리 구조
- 조직도

---

# 트리의 구현 방법

기본적으로 트리는 그래프의 한 종류이므로 그래프의 구현 방법으로 구현 가능하다.

1. 인접 배열 이용
    - 1차원 배열에 자신의 부모 노드만 저장하는 방법 → 트리의 각 노드는 부모 노드를 0 또는 1개만 갖는 특징을 이용한 구현
    - 2차원 정방행렬로 구현 → matrix[i][j] 표기로 i 노드에서 j 노드로 연결되어 있음을 표현
2. 인접 리스트 이용
    1. 엣지의 가중치가 없는 트리일 경우
        - `adjacency_list = [[] for _ in range(노드의 갯수))]`로 선언
        - i행 list의 원소들은 i 노드와 인접한 노드들의 `노드 번호`를 의미한다.
        - 결과적으로 각각의 행의 길이가 일정하지 않은 2차원 행렬이 만들어진다.
    2. 엣지의 가중치가 있는 트리일 경우
        - 마찬가지로 `adjacency_list = [[] for _ in range(노드의 갯수))]`로 선언
        - i행의 list의 원소들은 i 노드와 인접한 노드들의 `(노드 번호, 엣지 가중치)`의 리스트를 의미한다.
        - 마찬가지로 각각의 행의 길이가 일정하지 않은 2차원 행렬이 만들어진다.
        - 연산 편의상 adjacency_list의 첫 index를 1로 지정한다면, index 0은 사용하지 않는 대신 길이를 1 늘려서 선언한다.
            - ex) `adjacency_list = [[] for _ in range(노드의 갯수 + 1))]`

---

# 구현

아래 구현은 이진 트리 자료구조를 이용하는 BFS(Breadth-First Search) 알고리즘이다. 인접 리스트로 이진 트리를 구현하였다.

```python
class BFS:
    def __init__(self):
        self.graph = None   # 이진 트리
        self.visited = []
        self.queue = []

    def add_undirected_edge(self, node1, node2):
        if self.graph is None:
            raise Exception("There's no graph")
        self.graph[node1].append(node2)

    def make_graph(self, num_of_node, edge_list, start):
        graph = [[] for _ in range(num_of_node)]
        for node1, node2 in edge_list:
            graph[node1].append(node2)
            graph[node2].append(node1)

        for i in graph:
            i.sort()

        self.graph = graph
        self.visited = []
        self.queue = [start]

    def search(self):
        if self.graph is None:
            raise Exception("There's no graph")
        while self.queue:
            current_node = self.queue.pop(0)
            if current_node in self.visited:
                continue
            self.visited.append(current_node)
            for next_node in self.graph[current_node]:
                self.queue.append(next_node)

        return self.visited
```

- 단위 테스트

```python
import unittest

class TestBFS(unittest.TestCase):
    def setUp(self) -> None:
        self.bfs = BFS()
        self.edge_list = [(0, 1), (1, 2), (0, 2), (2, 3), (3, 4), (2, 4), (4, 0)]
        self.expected = [0, 1, 2, 4, 3]

    def tearDown(self) -> None:
        pass

    def test_bfs(self):
        self.bfs.make_graph(5, self.edge_list, 0)
        result = self.bfs.search()
        self.assertEqual(self.expected, result)
```

> 참고: [https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)