# Python_01_function

## 함수

함수의 선언은 def 키워드 활용

함수는 함수명()으로 호출



return 은 함수 안에서만 사용되는 키워드

함수는 return(반환값) 만나면 종료

return(반환값)으로 1개의 객체만 나옴(tuple... **dictionary)

 ```python
 def function(parameter):
     return
 
 function(argument)
 ```



`parameter` : 함수가 실행되면 내부에서 사용되는 식별자(이름)

`argument` : 함수에 전달해주는 값

function 앞에 () 괄호는 함수 실행을 의미

공백

return

return None

세 개는 같은 의미



함수는 하나의 값



함수 -> 모듈 -> 패키지 -> 라이브러리



함수에 기본 인자를 설정하면, 전달값 없을 때 기본값 출력



## map

map(function, iterable)

```python
a = [1.4, 2.2, 3.14, 4.7]
b = list(map(int, a))
print(b)
```

각 요소에 적용하고 싶은 '함수' 입력

함수에 iterable 대입



## filter

filter(function, iterable) : True 값만 반환

```python
result = list(filter(lambda x: x % 2, a))
print(result)
```



## zip

 함수 여러 iterable을 각 항목끼리 튜플로 묶어줌



## 재귀 함수

1개 이상의 base case가 존재하고, 수렴하도록 작성



## Lambda

lambda 파라미터: 리턴



### LEGB

bulit-in scope : 파이썬이 실행된 이후부터 영원히 유지

global scope : 모듈이 호출된 시점 이후 혹은 인터프리터가 끝날 때까지 유지

enclosed scope : 특정 함수의 상위 함수

local scope : 함수가 호출될 때 생성되고, 함수가 종료될 때까지 유지



L E G B 순서로 찾아 쓰는데 값 변경 xx

global, nonlocal 은 변경 가능한데, 오류 나오면 찾기 어려움



## 가변인수

```python
def function(parameter_1, ..., *parameters):  # parameter 앞에 * 붙이면 패킹
    return parameter_1, ..., parameters

function(positional_argument_1, ..., keyword_argument)
```

`parameter` 뒤에 `*parameters` 가능 `*parameters` 값은 튜플로 반환

`positional argument` 뒤에 `keyword argument` 가능



`*parameters`는 여러 개의 `positional argument`를 하나의 필수 `parameter`로 받아서 사용



**parameter, argument에 키, 값 지정하면 딕셔너리로 반환

함수가 임의의 개수 argument를 keyword argument로 호출될 수 있도록 지정 (딕셔너리 key : value)
