# 힙 (Heap)

---

# 힙의 개념

힙은 우선순위 큐(Priority Queue)의 한 종류이며, 완전 이진 트리로서 주로 우선순위를 기준으로 데이터를 처리할 때 사용하는 자료구조다. 

- 특징
    - 스택은 후입선출(FILO), 큐는 선입선출(FIFO)의 특징을 가지지만, 힙은 데이터가 들어오는 순서와 상관없이 우선순위가 높은 데이터가 먼저 나가는 특징이 있다.

        ![https://gmlwjd9405.github.io/images/data-structure-heap/data-structure-heap-compare.png](https://gmlwjd9405.github.io/images/data-structure-heap/data-structure-heap-compare.png)

        출처: [https://gmlwjd9405.github.io/images/data-structure-heap/data-structure-heap-compare.png](https://gmlwjd9405.github.io/images/data-structure-heap/data-structure-heap-compare.png)

    - 우선순위 큐 중에서 가장 효율적인 자료구조다.

        ![https://gmlwjd9405.github.io/images/data-structure-heap/data-structure-heap-priorityqueue.png](https://gmlwjd9405.github.io/images/data-structure-heap/data-structure-heap-priorityqueue.png)

        출처: [https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)

    - 힙은 반정렬 상태를 유지한다. 이진 트리의 레벨에 따라 대략적인 우선순위를 정렬한다. 이러한 상태로 인해 부모 노드의 값은 자식 노드의 값보다 항상 크다.
    - 힙은 최대 힙과 최소 힙 두 가지가 있다.
        - 최대 힙(Max Heap): 부모 노드의 값 ≥ 자식 노드의 값
        - 최소 힙(Min Heap): 부모 노드의 값 ≤ 자식 노드의 값

        ![https://gmlwjd9405.github.io/images/data-structure-heap/types-of-heap.png](https://gmlwjd9405.github.io/images/data-structure-heap/types-of-heap.png)

---

# 사용 사례

우선순위 속성이 있는 데이터의 순차적 처리를 위해 사용된다.

- 로드 밸런싱
- 작업 스케줄링

---

# 구현

구현은 '힙 정렬'에서 다룰 예정

---

> 참고: [https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)