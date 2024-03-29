# Segment Tree

- **구간 트리(Segment Tree)**: 노드가 일차원 배열의 구간 혹은 구간에 대한 쿼리 결과를 저장하는 이진 트리이다.



## 세그먼트 트리의 특징

<img src="https://user-images.githubusercontent.com/57662010/174529479-1d56eb49-762d-48cf-b4af-601571604ec4.jpg" alt="segment tree" width="70%;" />

- 세그먼트 트리의 루트는 배열 전체 구간 `[0, n-1]`을 표현한다.
- 트리의 왼쪽 자식과 오른쪽 자식은 각각 트리의 루트가 표현하는 구간의 오른쪽과 왼쪽 구간을 나타낸다.
- 세그먼트 트리의 말단은 길이가 `1`인 구간을 표현한다.
- 세그먼트 트리는 **완전 이진 트리**의 형태를 사용하며, 대개 **포화 이진 트리**의 형태를 사용한다.
  - 이 경우 트리의 높이가 `O(logn)`으로 균형 잡혀 있으므로 쿼리에 대한 값을 찾는데 시간 복잡도가 `O(logn)`이 된다.



## 세그먼트 트리의 표현

- 세그먼트 트리는 일차원 배열로 표현할 수 있다.
  - 루트 노드는 `0`번 인덱스에 저장한다.
  - 노드 `i`의 왼쪽 자손은 `2 * i`번 인덱스에 저장한다.
  - 노드 `i`의 오른쪽 자손은 `2 * i + 1`번 인덱스에 저장한다.



## 펜윅 트리

- **펜윅 트리(Fenwick Tree)** 또는 **이진 인덱스 트리(Binary Indexed Tree)**: **구간 합**을 빠르게 구하기 위해 필요 없는 구간은 저장하지 않는 세그먼트 트리이다.



<img src="https://user-images.githubusercontent.com/57662010/174531359-a3d856fe-be18-4922-98f8-a8dfe474cc52.jpg" alt="binary indexed tree" width="70%;" />

가령, 위 세그먼트 트리에서 `[4, 7]` 구간의 합은 `[0, 7]` 구간의 합에서 `[0, 3]` 구간의 합을 빼서 구할 수 있다. 이때 `[4, 7]` 구간의 합은 저장할 필요가 없다. 따라서 `회색`으로 칠해진 구간의 합만 저장해도 모든 구간의 합을 구할 수 있게 된다.



### 펜윅 트리의 표현

```python
# arr: 주어진 일차원 배열
# tree: 펜윅 트리
tree[i] = 오른쪽 끝 위치가 arr[i]인 구간의 합
```



#### 구간의 합 구하기

이때 `[0, i]` 구간의 합은 다음과 같이 구할 수 있다.

1. `i + 1`를 이진수로 바꾼다.
2. 이진수에서 켜져있는 최하위 비트를 하나 끄고, `1`를 뺀 인덱스에 접근하여 값을 구한다.
3. 구한 값들을 더한다.
4. 켜져있는 최하위 비트가 최상위 비트가 될 때까지 반복한다.



<img src="https://user-images.githubusercontent.com/57662010/174590783-1ec9950c-044f-4b2a-ba87-d4fafaba93d9.jpg" alt="인덱스의 패턴" width="70%" />

가령 `[0, 5]` 구간의 합을 구하고자 한다.

1. 5 + 1 = 6 = 110(2)이다. 6 - 1 = 5이므로 `tree[5]`의 값을 찾는다.
2. 110(2)에서 켜져있는 최하위 비트를 끄면 100(2) = 4이다. 4 - 1 = 3이므로 `tree[3]`이다.
3. 100(2)에서 켜져있는 최하위 비트가 최상위 비트가 되었으므로, 여태 찾은 값들을 모두 더한다. 
4. `tree[5] + tree[3]`



켜져있는 최하위 비트는 `S & (S - 1)`로 끌 수 있다. [비트 마스킹 - 가장 작은 원소 삭제하기](https://github.com/leegwae/algorithms/blob/main/bit-masking.md#%EA%B0%80%EC%9E%A5-%EC%9E%91%EC%9D%80-%EC%9B%90%EC%86%8C-%EC%82%AD%EC%A0%9C%ED%95%98%EA%B8%B0) 참고





#### 펜윅 트리 배열의 내용 변경하기

`arr[i]`를 변경한다고 하자. 그렇다면 `arr[i]`를 포함하는 모든 구간의 합 역시 변경해주어야한다. 다음과 같이 할 수 있다.

1. `i + 1`를 이진수로 바꾼다.
2. 이진수에서 켜져있는 최하위 비트를 스스로에게 더하고, `1`를 뺀 인덱스에 접근하여 원하는 값을 더하거나 뺀다.
3. 구한 인덱스가 배열의 범위를 넘을 때까지 반복한다.



가령 `arr[4]`의 값을 `2` 늘리고자 한다.

1. 4 + 1 = 5 = 101(2)이다. 5 - 1 = 4이므로 `tree[4]`의 값에 `2`를 더한다.
2. 101(2)에 켜져있는 최하위 비트는 1(2)이다. 101(2) + 1(2) = 110(2) = 6이다. 6 - 1 = 5이므로 `tree[5]`의 값에 `2`를 더한다.
3. 110(2)에 켜져있는 최하위 비트는 10(2)이다. 110(2) + 10(2) = 1000(2) = 8이다. 8 - 1 = 7이므로 `tree[7]`의 값에 `2`를 더한다.
4. `7`은 `arr` 배열의 마지막 인덱스이므로, 연산을 종료한다.



켜져있는 최하위 비트는 `S & -S`로 추출할 수 있다. [비트 마스킹 - 가장 작은 원소 찾기](https://github.com/leegwae/algorithms/blob/main/bit-masking.md#%EA%B0%80%EC%9E%A5-%EC%9E%91%EC%9D%80-%EC%9B%90%EC%86%8C-%EC%B0%BE%EA%B8%B0) 참고



### 펜윅 트리의 구현

- `arr[0] = 0`으로 할당하고 인덱스 `1`부터 수를 넣으면 펜윅 트리 연산을 할 때 인덱스를 `1` 더해줄 필요가 없다.



[예: 구간_합\_구하기.py](https://github.com/leegwae/problem-solving/blob/main/segment_tree/%EA%B5%AC%EA%B0%84_%ED%95%A9_%EA%B5%AC%ED%95%98%EA%B8%B0.py)
