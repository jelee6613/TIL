# Algorithm_06_Combination

## 포문 구현

```python
arr = [1, 2, 3, 4, 5]
N = len(arr)
ans = [0] * 2

for i in range(N-1):
    for j in range(i+1, N):
        ans[0], ans[1] = arr[i], arr[j]
        print(ans)
```

`arr`에서 순서없이 2개를 뽑는 경우의 수는 위와 같은 이중포문으로 구현할 수 있다. 다만,  2개 초과분을  뽑을 땐 포문을 무한히 늘리는 것도 무리가 있다.



## 재귀 구현

```python
arr = [1, 2, 3, 4, 5]
N = len(arr)
K = 2
ans = [0] * K

def combinations(start, level):
	
    if level == K:
        print(ans)
        return
    
    for i in range(start, N-K+level+1):
        ans[level] = arr[i]
        combinations(i+1, level+1)
        ans[level] = 0  # here
        
combinations(0, 0)
```



위와 같이 재귀로 구현하면  `arr`에서 순서 없이 `K`개를 뽑는 경우의 수를 구할 수 있다. `combinations` 함수에 `start`와 `level` 인자로 0을 넣는다. 

---

### 함수 내부 포문의 범위

`start`는 `K`개 뽑힐 각 결과물의 `level` 번째 인덱스에 들어갈 수 있는 `arr`의 인덱스 이상 범위이다.

`N-K+level+1`은 `K`개 뽑힐 각 결과물의 `level`번째 인덱스에 들어갈 수 있는 `arr`의 인덱스 미만 범위이다.

---



첫 포문때 `level`은 0 이고, `K`개 뽑힐 결과물(`ans`)의 `level`번째 인덱스에 <strong>포문 범위</strong>의 인덱스에 해당하는 `arr` 값을 `ans[level]` 에 저장한다. 

첫 결과로 `arr`의 인덱스가 순차적으로 저장되어 `[1, 2, 3]` 이 나온다. 이어서 `return`이 되고,  이전 함수인 `#here` 부분으로 돌아가면, `level` 은 `-= 1`이 되고, 포문이 돌면서 다음 인덱스 값이 들어간다. 