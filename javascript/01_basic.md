# JavaScript_01_Basic



## 필요성

브라우저 화면을 '동적'으로 만들기 위함

브라우저를 조작할 수 있는 유일한 언어



## 변수 선언 키워드

* `let` : 재할당 O, 재선언 X
* `const` : 재할당 X, 재선언 X
* `var` : 재할당 O, 재선언 O (호이스팅 특성으로 권장 X)



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
  * 문자열(String), 템플릿 리터럴 (따옴표 대신 backtick으로 표현) => ${ } 형태로 표현식 삽입 가능
  * Boolean
  * undefined(typeof => undefined)
  * null(typeof => object)



### 참조 타입(Reference type)

* 객체(object) 타입의 자료형
* 변수에 해당 객체의 참조 값이 담김
* 다른 변수에 복사할 때 참조 값이 복사됨



## 삼항연산자

```javascript
console.log('a' > 'A' ? '소문자가 더 큽니다' : '대문자가 더 큽니다')
// '소문자가 더 큽니다'

// 조건식 ? True일때 결과 : False일때 결과
```



## 조건문

### if

```javascript
if (condition) {
  // do something
} else if (condition) {
  // do something
} else {
  // do somethind
}
```



### switch

```javascript
const nation = 'Korea'

switch(nation) {
    case 'Korea': {
        console.log('안녕하세요~')
        break
    }
    default: {
        console.log('Hi~')
    }
}
```

swtich(expression)와 case문의 오른쪽 값이 같으면 해당하는 블록 스코프 실행, break가 없으면 break를 만나거나 default문을 만날 때까지 모든 case 실행





## 반복문

* while

* for

* for ... in : 주로 객체(object)의 속성(key)들을 순회할 때 사용 (객체 순회)

  ```javascript
  const capitals = {
      korea: 'seoul',
      france: 'paris',
      USA: 'washington D.C'
  }
  
  for (let capital in capitals) {
      console.log(capital) // korea, france, USA
  }
  ```

  

* for ... of : 반복 가능한(iterable) 객체를 순회하며 값을 꺼낼 때 사용 (배열 순회)

  ```javascript
  const capitals = ['seoul', 'paris', 'washington D.C']
  
  for (let capital of capitals) {
      console.log(capital) // seoul, paris, washington D.C
  }
  ```
