# 스택 (Stack)

---

---

# 스택의 개념

스택은 한 쪽 끝에서만 자료를 넣고 뺄 수 있는 LIFO(Last In First Out) 형식의 자료구조다.

## 특징

- LIFO의 특징에 따라 가장 최근에 스택에 추가된 데이터가 가장 먼저 제거된다.
- 배열과 달리 특정 위치의 데이터에 접근하기 위해서는 가장 최근의 데이터(top)부터 탐색해야 하므로 최대 O(n)의 시간복잡도를 가진다.
- 하지만 스택에서 데이터를 추가하거나 삭제하는 연산은 상수 시간에 가능하다.
- 배열처럼 원소들을 하나씩 옆으로 밀어줄 필요가 없다.

스택은 연결리스트로 구현할 수 있다. 연결리스트의 같은 방향에서 아이템을 추가하고 삭제하도록 구현한다.

---

# 사용 사례

재귀 알고리즘을 사용하는 경우 스택이 유용하다.

- 재귀 알고리즘
    - 재귀적으로 함수를 호출해야 하는 경우에 임시 데이터를 스택에 넣어준다.
    - 재귀함수를 빠져 나와 퇴각 검색(backtrack)을 할 때는 스택에 넣어 두었던 임시 데이터를 빼줘야 한다.
    - 스택은 이런 일련의 행위를 직관적으로 가능하게 해 준다.
    - 또한 스택은 재귀 알고리즘을 반복적 형태(iterative)를 통해서 구현할 수 있게 해준다.
- 웹 브라우저 방문기록 (뒤로가기)
- 실행 취소 (undo)
- 역순 문자열 만들기
- 수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사)
    - ex) 올바른 괄호 문자열(VPS, Valid Parenthesis String) 판단하기
- 후위 표기법 계산
    - ex)

    ![https://wayhome25.github.io/assets/post-img/cs/postfix_not.png](https://wayhome25.github.io/assets/post-img/cs/postfix_not.png)

    출처: https://github.com/ythwork

---

# 구현 및 단위 테스트

- 구현

```python
class MyStack:
    class StackNode:
        def __init__(self, data):
            self.next_node = None
            self.data = data

    def __init__(self):
        self.top_node = None
        self.size = 0

    def push(self, data):
        new_node = self.StackNode(data)
        new_node.next_node = self.top_node
        self.top_node = new_node
        self.size += 1

    def pop(self):
        if self.top_node is None or self.size == 0:
            raise Exception("There's no nodes")
        pop_node = self.top_node
        self.top_node = self.top_node.next_node
        self.size -= 1
        return pop_node.data

    def peek(self):
        if self.top_node is None or self.size == 0:
            raise Exception("There's no nodes")
        return self.top_node.data

    def is_empty(self):
        if self.top_node is None or self.size == 0:
            return True
        return False

    def print_all(self):
        current_node = self.top_node
        line = ''
        while current_node is not None:
            line += str(current_node.data) + ' '
            current_node = current_node.next_node
        print(line)
```

- 단위 테스트

```python
import unittest

class TestMyStackTest(unittest.TestCase):
    def setUp(self) -> None:
        self.stack = MyStack()

    def tearDown(self) -> None:
        pass

    def test_push(self):
        for a in range(100):
            self.stack.push(a)
        self.stack.print_all()

    def test_pop(self):
        with self.assertRaises(Exception):
            self.stack.pop()
        self.stack.push(100)
        self.stack.push('push push')
        pop_data = self.stack.pop()
        self.assertEqual('push push', pop_data)
        self.stack.pop()
        with self.assertRaises(Exception):
            self.stack.pop()

    def test_peek(self):
        with self.assertRaises(Exception):
            self.stack.peek()
        self.stack.push('push more!')
        self.stack.push(13)
        self.assertEqual(13, self.stack.peek())
        self.stack.pop()
        self.assertEqual('push more!', self.stack.peek())
        self.stack.pop()
        with self.assertRaises(Exception):
            self.stack.peek()

    def test_print_all(self):
        for a in range(10):
            self.stack.push('push{}'.format(a))
        self.stack.print_all()
```

[[자료구조] 스택(Stack)이란 - Heee's Development Blog](https://gmlwjd9405.github.io/2018/08/03/data-structure-stack.html)