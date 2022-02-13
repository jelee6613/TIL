# HTML&CSS_01_HTML

## HTML

Hyper Text Markup Language

웹 페이지를 **구조화** 하기 위한 언어



* html : 문서 최상위 요소
* head : 문서 메타데이터 요소 (제목, 스타일, 브라우저에 나타나지 않는 내용)
* body : 문서 본문 요소 (실제 화면 구성과 관련된 내용)



### 요소(Element)

`<h1>contents</h1>`

HTML의 요소는 시작 태그와 종료 태그 그리고 태그 사이에 위치한 내용으로 구성

태그(Element, 요소)는 컨텐츠(내용)를 감싸는 것으로 그 정보의 성격과 의미를 정의

요소는 중첩 가능



### 속성(Attribute)

`<a href="https://google.com"></a>`

속성으로 태그의 부가적인 정보 설정 가능



#### HTML Global Attribute

* id : 문서 전체에서 유일한 고유 식별자 지정
* class : 공백으로 구분된 해당 요소의 클래스의 목록
* style : inline 스타일
* data-* : 페이지에 개인 사용자 정의 데이터를 저장하기 위해 사용
* title : 요소에 대한 추가 정보 지정
* tabindex : 요소의 탭 순서



### 구조화



#### 시맨틱 태그

div 태그 대체

* header : 문서 전체나 섹션의 헤더(머리말 부분)
* section : 문서의 일반적인 구분, 컨텐츠의 그룹을 표현
* footer : 문서 전체나 섹션의 푸터(마지막 부분)



#### table

* thead(header) \<tr\> > \<th\>
* tbody(body) > \<tr\> > \<td\>
* tfoot(footer) > \<th\> > \<td\>

\<tr\>로 가로 줄을 구성하고 내부는 \<th\> 또는 \<td\>로 셀을 구성

colspan, rowspan 으로 셀 병합

```html
<tfoot>
  <tr>
    <td>총계</td>
    <td colspan="2">2명</td>
  </tr>
</tfoot>
```



#### form

정보(데이터)를 서버에 제출하기 위한 영역

* action : 입력받은 데이터를 처리할 서버 상의 스크립트 파일의 주소를 명시
* method : 입력받은 데이터를 서버에 전달할 방식 (GET 혹은 POST)
* enctype : method가 post인 경우 데이터의 유형



##### method

###### GET

body가 비어 있는 대신 파라미터가 주소창에 나오는 방식

주소창에 "?파라미터이름=파라미터값" 을 쿼리스트링이라 부르며, 공개되어도 전혀 문제 되지 않는 정보를 다룰 때 사용

용량 제한O, 주소창 노출O

거의 대부분의 페이지



###### POST

HTTP 프로토콜의 body에 파라미터가 넘어가는 방식

용량 제한X, 주소창 노출X

로그인 페이지, 글 작성 페이지, 회원가입 페이지, 파일 업로드 등



##### input

* name
* value
* required, autofocus, disabled, readonly, autocomplete

input type을 적절히 지정해줘야 UI 개선 (ex. type="password" 하면 유저는 숫자입력창 나옴)

체크박스 같은 경우 각 박스에 value 값 지정해야 해당 체크 박스에 따라 value 값 넘어감

text는 입력 값이 value 값으로 넘어감



###### input label

label을 클릭하여 input 자체의 초점을 맞추거나 활성화 가능

선택 영역이 늘어나 웹 / 모바일(터치) 환경에서 편하게 사용 가능

화면 리더기에서 label을 읽을 수 있기 때문에 유저친화적

```html
<label for="name">사용자</label>			 # for 속성과
<input type="text" id="name" name="name">  # id 속성이 상호 연관
```
