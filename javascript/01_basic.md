# JavaScript_01_Basic



## 필요성

브라우저 화면을 '동적'으로 만들기 위함

브라우저를 조작할 수 있는 유일한 언어



## 변수 선언 키워드

* let : 재할당 O, 재선언 X
* const : 재할당 X, 재선언 X
* var : 재할당 O, 재선언 O (호이스팅 특성으로 권장 X)



### 블록 스코프

* if, for, 함수 등의 중괄호{} 내부를 가리킴
* 블록 스코프를 가지는 변수는 블록 바깥에서 접근 불가능



## 데이터 타입

### 원시 타입(Primitive type)

* 객체(object)가 아닌 기본 타입
* 변수에 해당 타입의 값이 담김
* 다른 변수에 복사할 때 실제 값이 복사됨
* 종류
  * 숫자(Number, *NaN는 계산 불가능한 경우 반한되는 값)
  * 문자열(String)
  * Boolean
  * undefined(typeof => undefined)
  * null(typeof => object)



### 참조 타입(Reference type)

* 객체(object) 타입의 자료형
* 변수에 해당 객체의 참조 값이 담김
* 다른 변수에 복사할 때 참조 값이 복사됨



## 삼항연산자

조건식 ? true경우 값 : false경우 값

조건식이 true면 : 기준 왼쪽 값 출력, false면 : 기준 오른쪽 값 출력



## 반복문

* while
* for
* for ... in : 주로 객체(object)의 속성들을 순회할 때 사용
* for ... of : 반복 가능한(iterable) 객체를 순회하며 값을 꺼낼 때 사용