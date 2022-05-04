# JavaScript_02_Function



## 함수

* 매개변수와 인자의 개수 불일치 허용

* rest parameter(...)를 사용하면 정해지지 않은 수의 매개변수를 배열로 받음 (python의 *args와 유사)

  ```javascript
  const restOpr = function (arg1, arg2, ...restArgs) {
      return [arg1, arg2, restArgs]
  }
  
  restArgs(1, 2, 3, 4, 5) // [1, 2, [3, 4, 5]]
  restArgs(1, 2) // [1, 2, []]
  ```

* spread operator(...)를 사용하면 배열 인자를 전개하여 전달 가능

  ```javascript
  const spreadOpr = function (arg1, arg2, arg3) {
      return arg1 + arg2 + arg3
  }
  
  const numbers = [1, 2, 3]
  spreadOpr(...numbers) // 6
  ```




### 선언식 (declaration)

* 익명 함수 X
* 호이스팅 O

```javascript
function plus(a, b) {
    return a + b
}
```



### 표현식 (expression)

- 익명 함수 O
- 호이스팅 X
- Airbnb Style Guide 권장 방식

```javascript
const plus = function(a, b) {
    return a + b
}
```



### 화살표 함수 (Arrow Function)

* function 키워드 생략 가능
* 매개변수가 하나라면 () 생략 가능
* 몸통이 표현식 하나라면 {}와 return 생략 가능

```javascript
const arrow1 = function(name) {
    return `hello, ${name}`
}

// function 키워드 생략 가능
const arrow2 = (name) => { return `hello, ${name}`}

// 매개변수가 하나면 () 생략 가능
const arrow3 = name => { return `hello, ${name}` }

// 몸통이 표현식 하나라면 {}와 return 생략 가능
const arrow4 = name => `hello, ${name}`
```



## 메서드

- map : 배열의 각 요소에 콜백 함수를 실행해서 반환 값을 요소로 하는 새로운 배열 반환

  ```javascript
  const numbers = [1, 2, 3, 4, 5]
  
  const doubleNums = numbers.map(num => num*2)
  // doubleNums = [2, 4, 6, 8, 10]
  ```

  

- filter : 배열의 각 요소에 콜백 함수를 실행해서 반환 값이 참인 것만 모아서 새로운 배열 반환

  ```javascript
  const numbers = [1, 2, 3, 4, 5]
  
  const oddNums = numbers.filter(num => num%2)
  // oddNums = [1, 3, 5]
  ```

  

- reduce : 배열의 각 요소에 콜백 함수를 실행해서 반환 값을 acc에 누적 후 반환

  ```javascript
  const numbers = [1, 2, 3, 4, 5]
  
  const total = numbers.reduce((acc, num) => acc + num)
  // total = 15
  ```

  
