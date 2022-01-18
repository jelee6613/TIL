# Python_04_Comprehension

what ?

한 줄로 작성하는 표기법



why ?

가독성



How?

## If Comprehension

```python
a = int(input())

if a >= 0:
	number = a
else:
    number = -a

print(number)  # 정수의 절대값 출력
```

```python
a = int(input())

number = a if a >= 0 else -a

print(number)  # 정수의 절대값 출력
```





## List Comprehension

```python
list = []
for i in range(1, 4):
	list.append(i)  # append 는 값을 추가할 때, list에 i 값을 넣음

print(list)  # [1, 2, 3]
```

```python
list = [i for i in range(1, 4)]

print(list)  # [1, 2, 3]
```



## Dictionary Comprehension

```python
dict = {}
for i in range(1, 4):
    dict[i] = i * 2  # key(좌) 값에 value(우) 설정
    
print(dict)  # {1: 2, 2: 4, 3: 6}
```

```python
dict = {i : i * 2 for i in range(1, 4)}  # {key : value for i in range}

print(dict)  # {1: 2, 2: 4, 3: 6}
```



## 중첩 Comprehension

```python
num = []
for i in range(1, 31):
    if i % 2:
        num.append(i)

print(num)
```

```python
num = []
num = [i for i in range(1, 31) if i % 2]

print(num)
```



