# Algorithm_01_Array



## 알고리즘이란?

어떠한 문제를 해결하기 위한 절차



알고리즘 표현방법

* 슈도코드
* 순서도



무엇이 좋은 알고리즘인가?

 1. 정확성

 2. 작업량

    시간 복잡도: 실제 걸리는 시간을 측정, 실행되는 명령문의 개수를 계산

    빅-오(O) 표기법 : 시간 복잡도 함수 중에서 가장 큰 영향력을 주는 n에 대한 항만을 표시

 3. 메모리 사용량

 4. 단순성

 5. 최적성



## 배열(Array)

일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조



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
count_a = [0] * (max(a) - min(a) +1)  # a의 최대-최소의 차이만큼 배열 생성
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