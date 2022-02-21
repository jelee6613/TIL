# Algorithm_02_Sort



## 배열(Array)

일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조



## 정렬 

### 버블 정렬(Bubble Sort)

인접한 두 개의 원소를 비교하며 자리를 반복 교환하는 방식



```python
list = [3, 5, 2, 1, 4]

for i in range(len(list)-1, 0, -1):
    for j in range(i):
        if list[j] > list[j+1]:
            list[j], list[j+1] = list[j+1], list[j]
```



### 카운팅 정렬(Counting Sort)

항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘



```python
a = [3, 0, 5, 1, 0, 8]
count_a = [0] * (max(a)+1)  # a의 최대값 +1 만큼 배열 생성
sorted_a = [0] * len(a)  # 정렬된 배열의 길이는 a 와 동일

for i in range(len(a)):  # count_a 에 각 숫자 개수만큼 카운트
    count_a[a[i]] += 1

for i in range(len(count_a)-1):  # count_a 각 인덱스 값을 누계
    count_a[i+1] += count_a[i]   # 누계된 값은 각 위치에 해당하는 숫자의 마지막 자리

for i in range(len(a)-1, -1, -1):  # a 의 마지막 요소가 위치할 인덱스 자리
    count_a[a[i]] -= 1			   # sorted_a 배열에 할당
    sorted_a[count_a[a[i]]] = a[i]

print(sorted_a)
```



### 선택 정렬

```python
arr = [4, 2, 5, 1]

def select(arr, k):
    for i in range(len(arr)):
        minidx = i
        for j in range(i+1, len(arr)):
            if arr[minidx] > arr[j]:
                minidx = j
        arr[i], arr[minidx] = arr[minidx], arr[i]
    return arr[k-1]

print(select(arr, 2))
```

