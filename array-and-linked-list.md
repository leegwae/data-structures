# Array

**배열(Array)**는 동일한 자료형을 가진 데이터를 연속적인 메모리에 순차적으로 저장하는 선형 자료구조이다. 배열의 요소는 인덱스(index)를 통하여 접근할 수 있다.



## Array vs ArrayList

- Array는 인덱스로 값에 접근할 수 있는 선형 자료구조이다. 일반적으로 생성할 때 크기가 고정된 Static Array를 이른다.
- ArrayList는 크기를 동적으로 변경할 수 있는 Dynamic Array이다.

| 연산       | 시간복잡도 | 설명                                                         |
| ---------- | ---------- | ------------------------------------------------------------ |
| `insert()` | `O(n)`     | 삽입할 위치와 그 이후의 요소들을 한 칸씩 뒤로 당겨야한다.    |
| `delete()` | `O(n)`     | 삭제된 요소 이후에 있는 요소들을 한 칸씩 앞으로 당겨야한다.  |
| `arr[0]`   | `O(1)`     | 인덱스로 요소에 접근하므로 요소에 상수 시간에 접근할 수 있다. |



# Linked List

**연결 리스트(Linked List)**는 노드가 다른 노드에 대한 포인터를 가지고 연결되어있는 선형 자료구조이다.



### 단일 연결 리스트

단일 연결 리스트(signly-linked list)에서는 노드가 후속 노드에 대한 포인터를 가진다.

```python
# Definition for singly-linked list.
class ListNode:
	def __init__(self, val=0, next=None):
		self.val = val
		self.next = next


class LinkedList:
	def __init__(self):
		self.head = ListNode()

	def is_empty(self):
		return self.head.next is None

	def print(self):
		if self.is_empty():
			print('리스트에 노드가 없습니다')

		node = self.head.next

		while node:
			print(f'{node.val}', end='->')
			node = node.next
		print('NULL')

	def append(self, item: ListNode):
		node = self.head
		while node.next:
			node = node.next
		node.next = item

	def insert(self, item: ListNode, prev: ListNode):
		if prev.next:
			item.next = prev.next
		prev.next = item
```



### 단일 연결 리스트의 시간 복잡도

| 연산       | 시간 복잡도 | 설명                                                         |
| ---------- | ----------- | ------------------------------------------------------------ |
| `append()` | `O(n)`      | 마지막 노드를 탐색해야한다.                                  |
| `insert()` | `O(1)`      | 선행 노드가 알려져있다면 상수 시간에 삽입 연산이 가능하다.<br />(그렇지 않다면 선행 노드를 탐색해야한다.) |
| `delete()` | `O(1)`      | 선행 노드가 알려져있다면 상수 시간에 삭제 연산이 가능하다.<br />(그렇지 않다면 선행 노드를 탐색해야한다.) |
| `find()`   | `O(n)`      | 원하는 노드를 찾기 위해 연결 리스트의 헤드부터 선형 탐색해야한다. |

- **삽입, 삭제 연산에 반드시 선행 노드를 필요로 한다.** 이는 노드가 양방향으로 연결된 이중 연결 리스트로 해결할 수 있다.



### 이중 연결 리스트

**이중 연결 리스트(Doubly Linked List)**에서는 노드가 선행 노드를 가리키는 포인터와 후속 노드를 가리키는 포인터를 가진다. 선행 노드를 반드시 필요로 하는 단일 연결 리스트에 비해 삽입, 삭제 연산이 용이하나 추가적인 공간을 필요로 하고 연산이 복잡하다.



## Array vs LinkedList

- Array는 인덱스를 통해 요소에 O(1)로 접근할 수 있지만 ArrayList는 특정 노드에 접근하기 위해 순차 탐색이 필요하다.
- LinkedList는 크기가 동적으로 변경될 수 있어 Array에 비해 메모리 관리가 용이하다.
- LinkedList는 요소들을 앞이나 뒤로 미는 Array에 비해 삽입과 삭제가 용이하다.

