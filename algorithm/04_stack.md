# Algorithm_04_Stack



## 스택의 특성

물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조

스택에 저장된 자료는 선형 구조를 가짐 (자료 간의 관계가 1대1)

스택에 자료를 삽입, 반출 가능

후입선출



## 스택의 연산

### 삽입: push

저장소에 자료를 저장

```python
def push(item, size):
	global top
    top += 1
    if top == size:
        raise ValueError('넘쳤다.')
    else:
        stack[top] = item
        
size = 5
stack [0] * size
top = -1
push(10, size)
[10, 0, 0, 0, 0]
```



### 삭제: pop

저장소에서 자료를 역순으로 꺼냄

```python
def pop():
    global top
    if top == -1:
        raise ValueError('밑바닥이다.')
    else:
        top -= 1
        return stack[top+1]

size = 5
stack = [0] * size
top = -1
push(10, size)  # [10, 0, 0, 0, 0]
pop()  # [10, 0, 0, 0, 0], 보이는 건 같지만 top -= 1로 인해, 새로 push 하면 먹힘
```



isEmpty : 스택이 공백인지 아닌지를 확인하는 연산

peek : 스택의 top에 있는 item(원소)을 반환하는 연산



## Memoization

```python
def fibo(n):
    global memo
    if n >= 2 and len(memo) <= n:
        memo.append(fibo(n-1) + fibo(n-2))
    return memo[n]
    
memo = [0, 1]
```



## DP

Dynamic Programming, aka 기억하기 프로그래밍

```python
def fibo(n):
    f = [0, 1]
    
    for i in range(2, n+1):
        f.append(fibo(i-1)+fibo(i-2))
        
    return f[n]
```



깊이 우선 탐색(Depth First Search, DFS)

너비 우선 탐색(Breadth First Search, BFS)