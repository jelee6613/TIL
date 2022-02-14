# Algorithm_02



## 델타배열

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



## 비트 연산자



& : 비트 단위로 AND 연산

| : 비트 단위로 OR 연산

<< : 피연산자의 비트 열을 왼쪽으로 이동

\>\> : 피연산자의 비트 열을 오른쪽으로 이동



* `1 << n` : `2 ** n` 즉, 원소가 n 개일 경우 모든 부분집합의 수를 의미 + 선택
* `i & (1<<j)` : `i`  의 `j`번째 비트가 1인지 아닌지를 검사







비트연산자, 이진검색알고리즘, 버블과 선택정렬의 차이를 설명



from itertools import combinations



![image-20220214175123202](220214.assets/image-20220214175123202.png)