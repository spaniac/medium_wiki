# 큐 (Queue)

---

# 큐의 개념

먼저 집어 넣은 데이터가 먼저 나오는 FIFO(First In First Out) 구조로 저장하는 자료 구조

## 특징

- 스택과 마찬가지로 특정 데이터에 접근할 때 최대 n개의 데이터를 거쳐야 한다. (연결리스트로 구현 시)

큐 역시 연결리스트로 구현할 수 있다. 스택은 데이터의 입구와 출구가 같지만, 큐는 데이터의 입구와 출구가 다르다.

---

# 사용 사례

데이터가 들어간 순서대로 처리해야 할 필요가 있는 상황에 이용한다.

- 너비 우선 탐색(BFS, Binary-First Search)
    - 처리해야 할 노드의 리스트를 저장하는 용도로 큐를 사용한다.
    - 노드를 하나 처리할 때마다 해당 노드와 인접한 노드들을 큐에 다시 저정한다.
    - 노드를 접근한 순서대로 처리할 수 있다.
- 캐시(Cache) 구현
- 우선순위가 같은 작업 예약(인쇄 대기열)
- 선입선출이 필요한 대기열(티켓 카운터)

---

# 구현 및 단위 테스트

- 구현

```python
class MyQueue:
    class QueueNode:
        def __init__(self, data):
            self.data = data
            self.next_node = None

    def __init__(self):
        self.first_node = None
        self.last_node = None

    def add(self, data):
        new_node = self.QueueNode(data)

        if self.last_node is not None:
            self.last_node.next_node = new_node
        self.last_node = new_node
        if self.first_node is None:
            self.first_node = self.last_node

    def remove(self):
        if self.first_node is None:
            raise Exception("There's no nodes")
        data = self.first_node.data
        self.first_node = self.first_node.next_node
        if self.first_node is None:
            self.last_node.next = None
        return data

    def peek(self):
        if self.first_node is None:
            raise Exception("There's no nodes")
        return self.first_node.data

    def is_empty(self):
        return True if self.first_node is None else False

    def print_all(self):
        if self.first_node is None:
            print("There's no nodes")
        line = ""
        current_node = self.first_node
        while current_node is not None:
            line += str(current_node.data) + " "
            current_node = current_node.next_node
        print(line)
```

- 단위 테스트

```python
import unittest

class TestMyQueue(unittest.TestCase):
    def setUp(self) -> None:
        self.queue = MyQueue()

    def tearDown(self) -> None:
        pass

    def test_add_node(self):
        for a in range(100):
            self.queue.add(a)
        print(self.queue.print_all())

    def test_remove_node(self):
        with self.assertRaises(Exception):
            self.queue.remove()
        self.queue.add(['ase', 'fes'])
        self.assertEqual(['ase', 'fes'], self.queue.remove())
        with self.assertRaises(Exception):
            self.queue.remove()

    def test_peek_data(self):
        with self.assertRaises(Exception):
            self.queue.peek()
        self.queue.add(3)
        self.assertEqual(3, self.queue.peek())
        self.queue.add(['hello', 'world'])
        self.assertEqual(3, self.queue.peek())
        self.queue.remove()
        self.assertEqual(['hello', 'world'], self.queue.peek())
        self.queue.remove()
        with self.assertRaises(Exception):
            self.queue.remove()
        with self.assertRaises(Exception):
            self.queue.peek()

    def test_is_empty(self):
        self.assertTrue(self.queue.is_empty())
        self.queue.add(3)
        self.queue.add(['hello', 'world'])
        self.assertFalse(self.queue.is_empty())

    def test_print_all(self):
        self.queue.print_all()
        self.queue.add(1)
        self.queue.add(3)
        self.queue.add(['ase', 'fes'])
        self.queue.print_all()
```

> 참고: [https://gmlwjd9405.github.io/2018/08/02/data-structure-queue.html](https://gmlwjd9405.github.io/2018/08/02/data-structure-queue.html)