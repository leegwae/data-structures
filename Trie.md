# Trie

- **트라이(Trie)**: 문자열 탐색에 사용되는 트리 기반의 자료구조이다.
- 트라이의 노드는 자신의 `키값`과 `자식 트라이 노드들`의 배열(혹은 딕셔너리)를 프로퍼티로 가진다.



<img src="https://user-images.githubusercontent.com/57662010/175771943-f7a27333-6a21-4740-afc7-fa41e867251d.jpg" alt="trie" width="35%;" />

문자열 `'poem'`과 `'poet'`로 구성한 트라이이다.



## 트라이의 연산

- `insert(트라이, 문자열)`: 트라이에 문자열을 삽입한다.
- `search(트라이, 문자열)`: 트라이에 문자열이 있는지 탐색한다.
- `startsWith(트라이, 문자열)`: 트라이에 `문자열`로 시작하는 문자열이 있는지 탐색한다.



## 트라이의 구현

트라이는 파이썬의 `딕셔너리`를 사용하여 구현할 수 있다.



### 트라이 노드

```python
from typing import Optional, Dict


class TrieNode:
	def __init__(self, key: Optional[str]):
		self.key = key
		self.isTerminal = False
		self.children: Dict[str, TrieNode] = {}
```

트라이의 노드는 자신의 키값 `key`와 자식 트라이 노드의 딕셔너리 `children`, 트리에서 단말 노드인지 나타내는 `isTerminal` 불 변수를 프로퍼티로 가진다. `isTerminal`은 문자열 `S`가 트라이에 있을 때 `S`의 서브스트링을 판별하기 위해 사용한다. 가령, `abc`가 트라이에 있을 때 `search('ab')`는 `False`여야하기 때문이다. 순회를 끝낸 후에도 도착한 노드가 단말 노드가 아니라면(`isTerminal == False`) `ab`는 트라이에 있는 것이 아니다. `ab`로 시작하는 문자열이 있을 뿐이다.



### 트라이

```python
class Trie:
	def __init__(self):
		self.root = TrieNode(None)

	def insert(self, word: str) -> None:
		node = self.root

		for char in word:
			if char not in node.children:
				node.children[char] = TrieNode(char)
			node = node.children[char]

		node.isTerminal = True

	def search(self, word: str) -> bool:
		node = self.root

		for char in word:
			if char not in node.children:
				return False
			node = node.children[char]

		return node.isTerminal

	def startsWith(self, prefix: str) -> bool:
		node = self.root

		for char in prefix:
			if char not in node.children:
				return False
			node = node.children[char]

		return True
```

각각의 메서드들은 트라이 순회용 노드 `node`를 선언하여 루트부터 `children[키값]`에 접근하여 탐색을 진행한다.



### 전체 코드

[trei.py](https://github.com/leegwae/problem-solving/blob/main/trie/Trie.py)

```python
from typing import Optional, Dict


class TrieNode:
	def __init__(self, key: Optional[str]):
		self.key = key
		self.isTerminal = False
		self.children: Dict[str, TrieNode] = {}


class Trie:
	def __init__(self):
		self.root = TrieNode(None)

	def insert(self, word: str) -> None:
		node = self.root

		for char in word:
			if char not in node.children:
				node.children[char] = TrieNode(char)
			node = node.children[char]

		node.isTerminal = True

	def search(self, word: str) -> bool:
		node = self.root

		for char in word:
			if char not in node.children:
				return False
			node = node.children[char]

		return node.isTerminal

	def startsWith(self, prefix: str) -> bool:
		node = self.root

		for char in prefix:
			if char not in node.children:
				return False
			node = node.children[char]

		return True
```



## 트라이의 복잡도

트라이에 있는 문자열의 개수가 `N`, 가장 긴 문자열의 길이가 `L`이라고 하자.



### 시간 복잡도

- 최악의 경우 `O(L)`. 찾고자 하는 문자열의 길이만큼 노드를 옮기기 때문이다.



### 공간 복잡도

- 최악의 경우 문자열의 길이만큼 노드의 개수기 필요하고, 각각의 문자열이 겹치지 않는다면 `O(N * L)`
