# Java_04_Array



## 배열

- 같은 자료형의 데이터들의 모임
- 크기가 고정되어 있다(한번 생성된 배열의 크기는 수정 불가)
- 객체
- 배열로 선언된 변수들은 연속된 데이터 공간에 할당
- 배열의 요소를 참조하려면 배열이름과 int 유형의 인덱스(색인)를 사용



```java
int[] score = new int[5];  // int 타입 5개의 변수가 저장된 연속된 공간 주소를 저장

score[0] = 80;
score[1] = 75;
score[2] = 60;
score[3] = 100;
score[4] = 5;
```

- int[] : 타입의 한 종류이다. int 타입의 연속된 공간 주소를 저장



### 초기화

- {}를 활용하는 방식 : 배열 선언 시에만 설정 가능
  1차원 배열 : 배열유형 [] 배열명 = {값, .. 값};

  ```java
  int[] prime = {1, 2, 3};
  ```

  2차원 배열 : 배열유형 \[][] 배열명 = { {값1, 값2}, {값3, 값4} };

  ```java
  int[][] twoArr = { {1, 2}, {3, 4}, {5, 6} };
  ```

  

### for문으로 array의 max값 찾기

```java
int max_score = 0;

for(int i = 0; i < 5; i++) {
    if(score[i] > max_score) {
        max_score = score[i];
    }
}

System.out.printIn(max_score);
```

- for문에 `i < 5` 대신에 `score.length`를 사용할 수 있다.

  ```java
  for(int i = 0; i < score.length; i++)
  ```




### for-each

- for(원소 : 데이터의 모임)
  데이터의 모임에서 원소를 하나씩 꺼내서 작업을 수행한다.

```java
for(int n : score) {
    System.out.printIn(n);
}

// score의 변수를 하나씩 꺼낸다.
// n을 변경해도 score의 원소가 변하지 않는다.
// 읽기 전용
```





## 라이브러리

### java.util.Arrays

배열에 들어있는 원소를 한 눈에 볼 수 있다.

```java
import java.util.Arrays;

System.out.printIn(Arrays.toString(score));
// [80, 75, 60, 100, 5]
```



### Math.min & Math.max

```java
int[] intArray = {3, 20, 12, 5};

int max = Integer.MIN_VALUE;
int min = Integer.MAX_VALUE;

for (int i = 0; i < intArray.length; i++) {
    max = Math.min(intArray[i], max);
    min = Math.max(intArray[i], min);
}
```

