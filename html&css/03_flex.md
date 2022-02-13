# HTML&CSS_03_Flex

Inline <span> ex. input, img...

block <div> ex. h1~, p...

모든 요소는 좌측 상단을 향하는 네모



fixed : viewport 기준으로 고정 위치



## Float

* float: none; (기본값)
* float: left; (요소를 왼쪽으로 띄움)
* float: right; (요소를 오른쪽으로 띄움)



Float는 Normal Flow에서 벗어나 부동 상태(떠 있음)

### Clearing Float

부모요소에 Clearing Float를 해서 이후 요소는 Normal Flow 가지도록 설정

```html 
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}
```



## Flex

### 축

* main axis (메인 축)
* cross axis (교차 축)



### 구성 요소

* Flex Container (부모 요소)

```html
.flex-container {
  display: flex;    # flex item들이 놓여있는 영역
}					# display 속성은 flex 또는 inline-flex
```



* Flex Item (자식 요소)

컨테이너에 속해 있는 컨텐츠(박스)



### 속성

#### 배치 설정

* flex-direction: (row / column / row-reverse / column-reverse)

* flex-wrap: (wrap, 컨테이너 넘치면 다음 줄에 배치 / nowrap, 넘치지 않게 한 줄에 배치)

* flex-flow: flex-direction과 flex-wrap에 대한 값을 차례로 작성

  예시) flex-flow: column wrap;



#### 공간 나누기

* justyfy-content:

  (main axis)

* align-content:

  (cross axis)

  

#### 정렬

* align-items:

  (모든 아이템을 cross axis 기준으로)

* align-self: 

  (해당 컨테이너 말고 개별 아이템에 작성 및 적용)

  

연습 사이트 : flexboxfroggy.com
