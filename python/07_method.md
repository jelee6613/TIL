# Python_07_method



## .count(x)

s 에 등장하는 x 의 총수

```python
'apple'.count('p')  # 2

list = [1, '2', '1', '1']
list.count('1')  # 2
list.count(1)  # 1
```



## .find(x, start, end)

탐색

x의 첫번째 위치 반환, 없으면 -1 반환

str 시작과 끝 index 범위내에서 찾을 문자의 가장 빠른 위치의 인덱스 반환

start 와 end는 생략 가능

start 생략시 처음부터

end 생략시 끝까지



## .index(x)

x의 첫번째 위치 반환, 없으면 오류

```python
'apple'.index('p')
1
'apple'.index('k')
Error
```





## .split()

.split(sep = None, maxsplit = -1)

```
  split 함수는 `a.split()` 처럼 괄호 안에 아무 값도 넣어주지 않으면 공백(스페이스, 탭, 엔터 등)을 기준으로 문자열을 나누어 준다. 만약 `b.split(':')` 처럼 괄호 안에 특정 값이 있을 경우에는 괄호 안의 값을 구분자로 해서 문자열을 나누어 준다.

나눈 값은 리스트에 하나씩 들어간다.

https://wikidocs.net/13#count (출처: 02-2 문자열 자료형 - 점프 투 파이썬)
```



```python
print('ka k a    d'.split())
# ['ka', 'k', 'a', 'd']
```



## .replace(old, new[,count])

``` 
모든 부분 문자열 old가 new로 치환된 문자열의 복사본을 반환
선택적 인자 count가 주어지면, 앞의 count 개만 치환
https://docs.python.org/ko/3/library/stdtypes.html (출처: 파이썬 공식 라이브러리)
```

str 자체가 바뀌는 것은 아님



## .strip()

```python
sentence = "  I can do studying programming well  "
print(sentence)
print(sentence.strip())

#   I can do studying programming well  
# I can do studying programming well
```

특정한 문자들을 지정하면,

양쪽을 제거하거나(strip), 왼쪽을 제거하거나(lstrip), 오른쪽으 제거()

() 공백이면 기본값은 공백, 양 끝의 공백을 제거

str 자체가 바뀌는 것은 아님



## .join()

반복가능한(iterable) 요소들을 separator(구분자)로 합쳐 문자열 반환

numbers = [1, 2, 3, 4]

' '.join(map(str, numbers))



많이 쓰는 것 ) 어펜드, 팝, 카운트, 소트