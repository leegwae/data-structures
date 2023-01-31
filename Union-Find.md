# Union-Find

- **서로소 집합(disjoint set)**은 공통 원소가 없는 두 개 이상의 집합이다.
- **Union-Find**는 서로소 집합을 표현할 때 사용하는 자료구조이다.



## Union-Find의 연산

1. 초기화: 원소가 각각의 집합에 속하도록 초기화한다.
2. 합치기(union): 두 원소 A, B가 속한 집합을 하나로 합친다.
3. 찾기(find): 주어진 원소가 속하는 집합을 반환한다.

원소 A, B가 같은 집합에 속한다면 합치는 과정을 반복하여 서로소 집합을 만들 수 있다.



## Union-Find의 구현

1. 배열 사용하기: 찾기는 빠르지만 합치기가 느리다.
2. 트리 사용하기: 찾기는 비교적 느리지만 합치기가 빠르다.



### 배열 사용하기

```
belongsTo[i]=원소 i가 속하는 집합의 번호
```

1. 찾기: 인덱스를 통해 접근하여 주어진 원소가 속하는 집합을 구할 수 있으므로 O(1)로 구현할 수 있다.
2. 합치기: 두 집합 중 한쪽 집합에 속하는 원소를 옮기기 위해 for문을 돌아야하므로 O(n)으로 구현할 수 있다.



### 트리 사용하기

하나의 트리가 하나의 집합으로 표현된다. 자식 노드는 부모 노드에 대한 포인터를 가진다.

1. 찾기: 트리의 루트로 트리를 구분할 수 있으므로, 주어진 원소가 속한 트리의 루트를 구한다.
2. 합치기: 두 트리 중 한쪽 트리의 루트에 다른쪽 트리를 자손으로 넣는다.

```python
# 2. 찾기
def find(u):
	if parent[u] == u:
		return u

	return find(parent[u])


# 3. 합치기
def union(u, v):
	u, v = find(u), find(v)

	if u == v:
		return

	parent[u] = v


if __name__ == '__main__':
	N = int(input())
	# 1. 초기화
	parent = [i for i in range(N)]
```



그러나 이 경우 트리가 한쪽으로 기울어지는 문제가 발생할 수 있다.

```
union(0, 1)	# 0 -> 1
union(1, 2) # 1 -> 2
union(2, 3) # 2 -> 3
...
union(n-1, n) # n-1 -> n

0 -> 1 -> 2 -> 3 -> ... -> n-1 -> n
```

이때 찾기와 합치기 연산은 O(n)의 복잡도를 가진다.



#### union-by-rank 최적화

union-by-rank 최적화는 높이가 더 낮은 트리를 더 높은 트리의 자손으로 넣는 방법이다.



```python
# 트리의 레벨을 저장한다.
rank = [0] * N

# 3. 최적화된 합치기
def union(u, v):
	u, v = find(u), find(v)

	if u == v:
		return

	if rank[u] > rank[v]:
		u, v = v, u
	parent[u] = v
	if rank[u] == rank[v]:
		parent[v] += 1
```

