# Stack

- **스택(stack)**: 가장 최근에 들어온 데이터가 먼저 나가는 `후입선출(LIFO: Last-In-First-Out)`의 구조를 가진다.



## 스택의 연산

- `is_empty(스택)`: 스택이 비어있는지 검사한다.
- `push(스택, 요소)`: 스택에 요소를 추가한다.
- `pop(스택)`: 스택에서 가장 위에 있는 요소를 꺼내어 반환한다.
- `peek(스택)`: 스택에서 가장 위에 있는 요소를 (삭제없이) 반환한다.



## 스택의 구현

스택은 `연결 리스트`로 구현할 수 있다.

[Stack.py](https://github.com/leegwae/problem-solving/blob/main/stack/Stack.py)

```python
from typing import Optional, TypeVar

T = TypeVar('T')


class ListNode:
	def __init__(self, val: T, next: Optional['ListNode'] = None):
		self.val = val
		self.next = next


class Stack:
	def __init__(self):
		self.top = None

	def is_empty(self) -> bool:
		return self.top is None

	def push(self, item: T):
		self.top = ListNode(item, self.top)

	def pop(self) -> Optional[T]:
		if self.is_empty():
			return None

		val = self.top.val
		self.top = self.top.next

		return val

	def peek(self) -> Optional[T]:
		return None if self.is_empty() else self.top.val

```



## 스택의 시간 복잡도

| 연산        | 시간 복잡도 | 설명                                                         |
| ----------- | ----------- | ------------------------------------------------------------ |
| `push()`    | `O(1)`      | `top`으로 가장 위에 있는 요소를 가리키므로 상수 시간에 삽입 연산이 가능하다. |
| `pop()`     | `O(1)`      | `top`으로 가장 위에 있는 요소를 가리키므로 상수 시간에 삭제 연산이 가능하다. |
| `search(i)` | `O(n)`      | 연결 리스트로 구현되었으므로 상수 시간에 요소를 탐색할 수 없다. |



## 스택 응용하기

- 괄호 검사 [0912번_괄호.py](https://github.com/leegwae/problem-solving/blob/main/stack/9012_%EA%B4%84%ED%98%B8.py)



## 파이썬과 스택

파이썬의 `리스트`는 스택의 연산을 지원한다.



| 연산           | 시간 복잡도 | 설명                                                         |
| -------------- | ----------- | ------------------------------------------------------------ |
| `append(item)` | `O(1)`      | 가장 뒤에 요소를 삽입하므로 상수 시간에 삽입 연산이 가능하다. |
| `pop()`        | `O(1)`      | 가장 마지막에 있는 요소를 삭제하고 반환하므로 상수 시간에 삭제 연산이 가능하다. |
| `stack[-1]`    | `O(1)`      | 인덱스로 요소에 접근하므로 가장 위에 있는 요소에 상수 시간에 접근할 수 있다. |

