# Django_01_basic



Static web page: 정적 웹페이지

Dynamic web page: 동적 웹페이지



## What

Python 으로 작성된 오픈 소스 Web Framework

웹 페이지 개발 과정에서 겪는 어려움을 줄이는 것이 주 목적

데이터베이스 연동, 템플릿 형태의 표준, 세션 관리, 코드 재사용 등



## Why

검증된 python 언어 기반 Web Framework

Django는 MTV (model-template-view) pattern

원래는 MVC (model-view-controller) pattern



<img src="https://github.com/jelee6613/TIL/blob/master/img/image-20220302092543448.png" />



## MTV pattern

### Model

응용프로그램의 데이터 구조를 정의, 데이터베이스 기록 관리(추가, 수정, 삭제)



### Template (view)

파일 구조나 레이아웃을 정의

실제 내용을 보여주는데 사용 (presentation)



### View(controller)

http 요청을 수신, http 응답을 반환

model을 통해 요청을 충족시키는데 필요한 데이터에 접근

template에게 응답의 서식 설정을 맡김



## 기본 루틴

#### 1. 가상환경 생성 및 활성화

`$ python -m venv venv`

`$ source venv/Scripts/activate`

(venv) 확인



#### 2. django 설치

`$ pip install django==3.2.12` (가상환경에 설치, 전역X)

`$ pip list` (확인)



#### 3. 프로젝트 생성

`$ django-admin startproject <pjt 이름> .`

프로젝트 이름은 python 이나 django 에서 사용중인 키워드 X

\'-' (하이픈) 도 사용 X, ex) Django, text, class, seoul-lee



#### 4. django 서버 시작하기(활성화)

`$ python manage.py runserver`

Ctrl + 왼쪽마우스로 로켓확인



#### 5. Application 생성 (이름은 복수형 권장)

`$ python manage.py startapp <articles>`   <= 이름



#### 6. 프로젝트에 앱등록하기 (반드시 앱 생성 후 등록)

프로젝트 디렉토리의 settings.py > INSTALLED APPS 에 apllication 이름 등록
