# Python_09_Class



객체(object) = 속성 + 기능(Method)



절차지향 예시

a = 3

a = 5



객체지향 예시

a.sort()

a.reverse()



## 클래스 생성

클래스 정의 : class Person:

인스턴스 생성 :  jelee = Person()

메소드 호출(행동) : jelee.method()

속성 : jelee.attribute



is 는 동일한 객체를 가리키는 지, id 값이 같은지 확인

== 는 값이 같은지, 같은 걸 가리키는 지는 확인 X



## 생성자 메소드

def \__init__(self, name, age):

​		self.name = name

​		self.age = age



## 소멸자 메소드

def \__del__(self):



---



인스턴스 생성

young = Person('영택', 100)

young.name = '영택'

young.age = 100



인스턴스 삭제

del young



클래스 메서드 : 클래스를 조작할 때

@classmethod



스태틱 메서드 : 클래스나 인스턴트를 조작할 생각은 없는데 함수를 쓸 때

@staticmethod



```python
def \__init__(self, name, age, student_id):

	super().\__init__(name, age) 			# super()는 상위 클래스의 init 값을 불러옴. 단, 현재 클래스에 새로운 값 쓰면 덮어쓸 수 있음
	self.studeunt_id = student_id			# 상위 클래스에 없던 student_id 추가
```

