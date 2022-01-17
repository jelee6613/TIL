# Python_자료형

## 변수(Variable)

객체(object)를 참조하기 위해 사용되는 이름

객체(object) : 숫자, 문자, 클래스 등 값을 가지고 있는 모든 것

파이썬은 객체지향 언어이며, 모든 것이 객체로 구현되어 있음

동일 변수에 다른 객체를 언제든 할당할 수 있기 때문에, 변수라고 불림

**=**  : 할당(assignment)

`type()` : 변수에 할당된 값의 타입

```python
x = 1, y = 2
x = x + y  # 우변을 좌변으로 할당
x = 3
```



## 주석(Comment)

```python
``` ```
""" """
#
Ctrl + /
```



## Container

### Sequence(순서)

문자열, 수치 등을 관리하기 위한 자료형으로 순서 개념 O

배열 형식 구조로 인덱스를 이용해 데이터 접근

인덱스 값은 0부터 시작

연결이나 반복을 위해 +, * 연산자 사용 가능

#### String

문자열의 나열

불변(immutable), 순회(iterable)

#### List []

순서가 있는 0개 이상의 객체를 참조하는 자료형

가변(mutable), 순회(iterable)

#### Tuple ()

순서가 있는 0개 이상의 객체를 참조하는 자료형

불변(immutable)

#### Range

불변

### Non - Sequence

문자열, 수치 등을 관리하기 위한 자료형으로 순서 개념 X

순서가 없기 때문에 인덱스 이용 X

#### Dictionary {}

순서가 없는 키-값(key-value) 쌍으로 이루어진 객체를 참조하는 자료형

가변(mutable), 순회(iterable)

key는 고유하며 중복 불가 (str, int, float, boolean, tuple, range) **list X**

value는 중복 가능, 모든 값으로 설정 가능



#### Set

순서가 없는 0개 이상의 *해시가능한* 객체를 참조하는 자료형

중복값 제거

가변(mutable) 순회(iterable)

