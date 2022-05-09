# Vue_01_Basic



## SFC (Single File Component)

- Vue의 컴포넌트 기반 개발의 핵심 특징
- 하나의 컴포넌트는 .vue 확장자를 가진 하나의 파일 안에서 작성되는 코드의 결과물
- 화면의 특정 영역에 대한 HTML, CSS, JavaScript 코드를 하나의 파일(.vue)에서 관리
- .vue 확장자를 가진 싱글 파일 컴포넌트를 통해 개발하는 방식
- Vue 컴포넌트 === Vue 인스턴스 === .vue 파일
  Vue 컴포넌트는 `const app = new Vue({...})`의 `app`을 의미하며 이는 Vue 인스턴스
  - 컴포넌트 기반의 개발이 반드시 파일 단위로 구분되어야 하는 것은 아님
  - 단일 .html 파일 안에서도 여러 개의 컴포넌트 개발 가능



장점 : 변수 관리가 용이하며 기능 별로 유지 & 보수 비용 감소

단점 : 처음 개발을 준비하는 단계에서 시간이 많이 듬





## Node.js

- 자바스크립트를 브라우저가 아닌 환경에서도 구동할 수 있도록 하는 자바스크립트 런타임 환경



### NPM (Node Package Manage)

- 자바스크립트 언어를 위한 패키지 관리자
  - Python에 pip가 있다면 Node.js에는 NPM
  - pip와 마찬가지로 다양한 의존성 패키지를 관리
- Node.js의 기본 패키지 관리자
- Node.js 설치 시 함께 설치됨



#### Quick Start

1. `$ npm install -g @vue/cli` => '-g' : 전역 설치
2. `$ vue create <app name>` => 프로젝트 생성
3. `$ npm run serve` => 프로젝트 디렉토리로 이동한 뒤 서버 실행



### Node.js & Babel & Webpack

Vue CLI는 자동으로 Babel, Webpack 초기 설정

- Node.js : JavaScript를 브라우저 밖에서 실행할 수 있는 새로운 환경
- Babel : 최신 코드를 과거 코드로 번역
- Webpack : 모듈 의존성 문제를 해결해주는 작업을 Bundling이라 하는데, 그 중 하나가 Webpack