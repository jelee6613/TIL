# Algorithm_03_delta



## 2차원 배열

* 1차원 List를 묶어놓은 List
* [[0, 1, 2, 3], [4, 5, 6, 7]]



```python
# 지그재그 순회 (N*N)
for row in range(N):
    for col in range(N):
        arr[row][col + (N-1-2*col) * row%2]
```



## 델타 탐색

```python
N = 3
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]  # N * N 배열

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

for row in range(N):
    for col in range(N):
        for i in range(4):  # dx, dy 요소 개수
            new_x, new_y = row+dx[i], col+dy[i]
            if N > new_x >= 0 and N > new_y >= 0:
                print(arr[new_x][new_y])

# 배열의 각 요소를 순회하며 인접 상좌하우 요소 출력
            
```



## 전치 행렬

```python
for row in range(N):
    for col in range(N):
        if row < col:
			arr[row][col], arr[col][row] = arr[col][row], arr[row][col]
```



## 비트 연산자

& : 비트 단위로 AND 연산

| : 비트 단위로 OR 연산

<< : 피연산자의 비트 열을 왼쪽으로 이동

\>\> : 피연산자의 비트 열을 오른쪽으로 이동



* `1 << n` : `2 ** n` 즉, 원소가 n 개일 경우 모든 부분집합의 수를 의미 + 선택
* `i & (1<<j)` : `i`  의 `j`번째 비트가 1인지 아닌지를 검사



## 조합

`from itertools import combinations`

