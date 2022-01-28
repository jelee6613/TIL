# Python_02_Class



`__str__` : display name 보여지는 이름

`__repr__` : username 로그인 id

`print` 함수 사용하면 `return` 값 출력
        

```python
def __gt__(self, other):
    return self.age > other.age

def __eq__(self, other):
    return self.age == other.age
```



## @classmethod

클래스메소드

class명.method()

인스턴스도 접근 가능하지만(사용X 자제), self가 인스턴스여도 결과는 클래스의 값으로 나온다. 

(인자 없어도 자동으로 부모 클래스) 엄마 지갑은 하나뿐인 엄마의 것이기 때문에



## instance method

인스턴스 메소드

클래스도 접근 가능하지만(사용X 자제), 인자로 인스턴스 지정 해줘야한다. (자식은 많기 때문에)



## @staticmethod

정적 메소드 

자동으로 채워지지 않는다.



## @property

getter 메소드는 값을 조회.탐색 하는 성격



## @object.setter

setter 메소드는 값을 설정,변경 하는 성격