# Vue_03_Router



## Vue Router

- Vue.js 공식 라우터
- 라우트(route)에 컴포넌트를 매핑한 후, 어떤 주소에서 렌더링할 지 알려줌
- SPA 상에서 라우팅을 쉽게 개발할 수 있는 기능을 제공



## Start

1. 프로젝트 생성 및 이동

   ```bash
   $ vue create <project name>
   $ cd <project name>
   ```

   

2. Vue Router plugin 설치 (Vue CLI 환경) => 기존에 진행하던 프로젝트 있으면 App.vue 덮으므로 백업 권장

   ```bash
   $ vue add router
   ```

   

3. Commit 여부

4. History mode 사용 여부

   

## 설치 후 생긴 것

- index.js : 라우트에 관련된 정보 및 설정이 작성 되는 곳
- router-link : 
  1. 사용자 네비게이션을 가능하게 하는 컴포넌트 (App.vue에 생성)
  2. HTML5 히스토리 모드에서 클릭 이벤트를 차단하여 브라우저가 새로고침 하지 않도록 함
  3. 기본 GET 요청을 보내는 이벤트를 제거한 형태로 구성되어 기존 a 태그와 조금 다름
- router-view :
  1. 주어진 라우트에 대해 일치하는 컴포넌트를 렌더링하는 컴포넌트