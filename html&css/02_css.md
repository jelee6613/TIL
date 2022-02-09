# CSS_01_Basic

## CSS

Cascading Style Sheets

스타일을 지정하기 위한 언어

선택하고, 스타일을 지정한다.



CSS 정의 방법

* 인라인(inline)
* 내부 참조(embedding) - \<style\>
* **외부 참조(link file)** - 분리된 CSS 파일



* nth-child(n) : n번째 자리에 해당 요소가 있다면 기능
* nth-of-type(n) : 특정 요소 중 n번째 요소에 기능



### 크기 단위

* px : 픽셀의 크기는 변하지 않기 때문에 **고정적인** 단위
* % : 백분율 단위, **가변적인** 레이아웃에서 자주 사용
* em : 바로 위, 부모 요소를 상속 받아 상대적인 사이즈를 가짐
* rem : 최상위 요소(html)의 사이즈를 기준으로 배수 단위를 가짐
* viewport : vw, vh, vmin, vmax 디바이스의 viewport 기준으로 상대적 사이즈 결정



기본적으로 모든 요소의 box-sizing은 content-box

border 까지의 너비를 설정하고 싶다면 `box-sizing: border-box;` 



### Display

* display: block (div / ul, ol, li / p / hr / form)

  줄 바꿈이 일어나는 요소

  화면 크기 전체의 가로 폭을 차지한다.

  블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음

  

* display: inline (span / a / img / input, label / b, em, i, strong)

  줄 바꿈이 일어나지 않는 행의 일부 요소

  content 너비만큼 가로 폭을 차지한다.

  width, height, margin-top, margin-bottom을 지정할 수 없다.

  상하 여백은 line-height로 지정한다.

  *단, img는 너비 높이 설정 가능*

  

* display: inline-block

  block과 inline 레벨 요소의 특징을 모두 가짐

  한 줄 표시 가능, width, height, margin 속성 지정 가능

  

* display: none

  공간차지 X, 화면표시X

  (visibility: hidden은 공간차지O, 화면표시 X)



### CSS position

* relative : 상대 위치
* absolute : 절대 위치
* fixed : 고정 위치
