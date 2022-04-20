# Recursion

**재귀(recursion)**는 문제를 작은 단위로 나누어/정의하여 해결하는 것이다. 



## 재귀 함수

재귀 함수는 base case를 만날 때까지 자기 자신을 호출한다.



### 예: 1부터 n까지의 합 구하기

```python
int sum(int n) {
    if (n == 1) return 1;
    
    return sum(n - 1) + n;
}
```



### 예: 피보나치 수열

```c
int fib(int n) {
    if (n == 0 || n == 1) return n;
    
    return fib(n - 1) + fib(n - 2);
}
```



## 재귀와 반복

반복으로 `sum` 함수를 작성하면 다음과 같다.

```c
int sum(int n) {
    if (n == 1) return 1;
    
    int sum = 0;

    for (int i = 1; i <= n; i++) {
        sum += i;
    }
    
    return sum;
}
```



재귀의 장점은 아래와 같다.

- 재귀적인 문제를 풀 때 용이하다.
- 가독성이 반복을 사용하여 작성하였을 때 보다 좋다.

재귀의 단점은 아래와 같다.

- 함수 호출은 오버헤드를 발생시킨다.
  - 원래의 실행 문맥으로 돌아가기 위하여 시스템 스택을 사용한다. 메모리 사용 측면에서 비효율적이다.
- 반복에 비하여 수행 속도가 느리다.



## 참고

[알고리즘 스터디-recursion](https://theubermensch.tistory.com/195?category=880434)

