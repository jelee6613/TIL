# Python_03_Container

## Container

다중 데이터, 하나 이면서 동시에 각각



### Sequence(순서)

**시퀀스형 컨테이너**

문자열, 수치 등을 관리하기 위한 자료형으로 순서 개념 O

배열 형식 구조로 인덱스를 이용해 데이터 접근

인덱스 값은 0부터 시작

연결이나 반복을 위해 +, * 연산자 사용 가능

주의! 순서가 있다는 것이 정렬(sorted)이라는 의미는 아님

#### String

* immutable (불변형)
* iterable (순회)

문자열의 나열



#### List []

* mutable(가변형)
* iterable(순회)

순서가 있는 0개 이상의 객체를 참조하는 자료형



#### Tuple ()

* immutable (불변형)

순서가 있는 0개 이상의 객체를 참조하는 자료형

하나의 항목으로 구성된 튜플은 생성 시 값 뒤에 쉼표 ex) a = (1, )



#### Range

* Immutable (불변형)

range(b)

0부터 b-1 까지

range(a, b)

a부터 b-1까지

range(a, b, c)

a부터 b-1까지 c만큼  # c가 음수면 역순

b 보다 a 가 크면 c는 음수여야 함

정수의 시퀀스를 나타내기 위해 사용

---



### Associative Container

**비시퀀스형 컨테이너**

문자열, 수치 등을 관리하기 위한 자료형으로 순서 개념 X

순서가 없기 때문에 인덱스 이용 X



#### Dictionary {}

* mutable (가변형)
* iterable (순회)

{Key1: Value1, Key2: Value2, Key3: Value3, ...}

순서가 없는 키-값(key-value) 쌍으로 이루어진 객체를 참조하는 자료형

key는 고유하며 중복 불가 (**str**, int, float, boolean, tuple, range) **list X**

value는 중복 가능, 모든 값으로 설정 가능



#### Set

* mutable (가변형)
* iterable (순회)

{value1, value2, value3}

순서가 없는 0개 이상의 *해시가능한* 객체를 참조하는 자료형

**중복값 제거**

빈 세트 만드려면 set() 사용, {}는 불가능

합집합(`|`), 차집합(`-`), 교집합(`&`)

