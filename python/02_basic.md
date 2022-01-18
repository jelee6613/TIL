# Python_02_Basic

## 원시 자료형



### 불린형 (Boolean Type)

True/False

### 수치형 (Numeric Type)

`int` (정수, integer)

`float` (부동소수점, 실수, floating point number)

​	값 비교하는 과정에서 실수 주의

`complex` (복소수, complex number)

​	실수와 허수부

​		ex) 3+4j

### 문자열 (String Type)

### None

값이 없음을 표현하기 위한 타입



## String interpolation

### %-formatting

​	%d : 정수

​	%f : 실수

​	%s : 문자열

```python
name = '이종은'
age = 28
print('%s의 나이는 %d살 입니다.' %(name, age))
이종은의 나이는 28살 입니다.
```



### str.format()

```python
name = '이종은'
age = 28
print('{}의 나이는 {}살 입니다.' .format(name, age))
이종은의 나이는 28살 입니다
```



### f-strings

```python
name = '이종은'
age = 28
print(f'{name}의 나이는 {age}살 입니다.')
이종은의 나이는 28살 입니다.
```

