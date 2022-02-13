# Python_08_Error & Exception

## 디버깅

* print 문 활용 - 특정 함수 결과, 반복/조건 결과 등 나눠서 생각
* 개발 환경(text editor, IDE) 등에서 제공하는 기능 활용 : breakpoint, 변수 조회
* Python tutor 활용 (단순 파이썬 코드인 경우)
* 뇌컴파일, 눈디버깅

## 에러 (Error)

### 문법 에러 (Syntax Error)

SyntaxError가 발생하면, 파이썬 프로그램은 실행 X

파일이름, 줄번호, ^문자를 통해 파이썬이 코드를 읽어 나갈 때(parser) 문제가 발생한 위치를 표현

줄에서 에러가 감지된 가장 앞의 위치를 가리키는 캐럿(caret)기호(^)를 표시

## 예외 (Exception)

* 실행 도중 예상치 못한 상황을 맞이하면, 프로그램 실행 멈춤 (문장이나 표현식이 문법적으로 올바르더라도 발생하는 에러)
* 실행 중에 감지되는 에러들을 예외(Exception)라고 부름
* 예외는 여러 타입(type)으로 나타나고, 타입이 메시지의 일부로 출력 (NameError, TypeError...)
* 모든 내장 예외는 Exception Class를 상속받아 이뤄짐
* 사용자 정의 예외를 만들어 관리할 수 있음

### 예외 처리

* try 문(statement) / except 절(clause)을 이용하여 예외 처리 가능
* try문 : 오류가 발생할 가능성 있는 코드 실행 => 예외가 발생되지 않으면 except 없이 실행 종료
* except문 : 예외가 발생하면, except절 실행 => 예외 상황을 처리하는 코드를 받아서 적절한 조치를 취함



**주의사항** : try문은 반드시 한 개 이상의 except문이 필요



예외 처리 예시_1

```python
try:
    num = input()
    print(100/int(num))
except ValueError:
    print('숫자가 아닙니다.')
except ZeroDivisionError:
    print('0으로 나눌 수 없습니다.')
except:
    print('에러는 모르지만 에러가 발생하였습니다.')
    
 #  에러 별로 별도의 예외 처리
 #  except 문은 순차적으로 진행되므로, 가장 작은 범주부터 예외 처리!
```



예외 처리 예시_2

```python
try:
    f = open('file.txt')
except FileNotFoundError:
    print('해당 파일이 없습니다.')
else:
    print('파일을 읽기 시작합니다.')
    print(f.read())
    print('파일을 모두 읽었습니다.')
finally:
    print('파일 읽기를 종료합니다.')
    
  # try : 코드 실행
  # except : try 문에서 예외 발생 시 실행
  # else : try 문에서 에외 발생하지 않으면 실행
  # finally : 예외 발생 여부와 관계없이 항상 실행
```



예외 처리 예시_3

```python
try:
    empty_list = []
    print(empty_list[-1])
except IndexError as err:
    print(f'{err}, 오류가 발생했습니다.')
    
    # list index out of range, 오류가 발생했습니다.
    
  # as 키워드 사용하면 원본 에러 메시지 사용 가능
```



### raise

raise를 통해 예외를 강제로 발생

raise <표현식> (메시지)

```python
raise ValueError('값 에러 발생')
  # ValueError: 값 에러 발생
```



### assert

assert를 통해 예외를 강제로 발생

assert는 상태를 검증하는데 사용되며, 무조건 AssertionError가 발생

일반적으로 디버깅 용도로 사용

assert <표현식>, <메시지>

표현식이 False인 경우, AssertionError

```python
assert len([1, 2]), '길이가 1이 아닙니다.'
  # AssertionError: 길이가 1이 아닙니다.
```

