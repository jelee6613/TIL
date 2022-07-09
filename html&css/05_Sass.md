# HTML&CSS_05_Sass



공식문서 : https://sass-guidelin.es/ko/



## Quick Start

1. ```bash
   $ npm i sass
   $ npm i sass-loader@10
   ```

2. ```vue
   <style lang="scss">
   
     // ...
   
   </style>
   ```

3. ```vue
   <style>
   $main_color: rgb(256, 256, 256);
   
   body {
     background-color: $main_color;
   }
   </style>
   ```



## Sass

Sass는 기초 언어에 힘과 우아함을 더해주는 CSS의 확장이다.



## Sass 혹은 SCSS

Sass는 처음에 들여쓰기를 특성으로 구문을 작성했는데, 보다 CSS와의 차이를 좁히기 위해 중괄호, 세미콜론 등을 유지한 SCSS가 있다.



## 스타일가이드

### 구문 & 서식

- 탭 대신 스페이스 두 칸(2) 들여쓰기;
- 이상적인 행의 너비는 80글자;
- 적절하게 쓰인 여러 행의 CSS 규칙;
- 공백의 의미 있는 사용

```scss
// Good
.foo {
  display: block;
  overflow: hidden;
  padding: 0;
}

// Bad
.foo {
    display: block; overflow: hidden;
    
    padding: 0 lem;
}
```



### 문자열

- 스타일시트의 맨 위에 `@charset` 지시문을 선언하는 것을 적극적으로 추천합니다.
- CSS 식별자로 적용되지 않는 한, 문자열은 작은따옴표를 사용하여 인용되어야 합니다. URL도 마찬가지입니다.



### 숫자

- Sass는 숫자, 정수, 부동 소수점을 구분하지 않으므로 뒤따르는 0은 생략해야 합니다. 그러나 앞장서는 영(0)은 가독성에 도움이 되므로 추가해야 합니다.
- 길이가 영(0)이면 단위가 없어야 합니다.
- 단위 조작은 문자열 연산이 아닌 산술 연산으로 생각해야 합니다.
- 가독성을 높이기 위해 최상위 계산은 괄호로 묶어야 합니다. 또한, 복잡한 수학 연산은 더 작은 덩어리로 나눌 수 있습니다.
- 매직넘버는 코드 유지 관리를 크게 해치므로 항상 피해야합니다. 의심스러울 때는, 의심스러운 값을 광범위하게 설명하세요.



### 색

- 색은 가능하면 HSL, RGB, 16진수(소문자 및 축약형) 순으로 표현해야 합니다. 색 키워드는 피해야 합니다.
- 색상을 밝게 하거나 어둡게 할 때는 `darken(..)` 이나 `lighten(..)` 대신 `mix(..)`를 선호합니다.



## Vue에서 전역 설정하기

1. _variabled.scss 파일 생성

   - _가 붙은 scss 파일은 변수만을 저장하는 scss파일로 인식

   - src/assets/scss에 _variabled.scss 파일을 생성하고 그 안에 변수를 관리

   - ```scss
     // src/assets/scss/_variabled.scss
     
     $nav_color: #26282B;
     $nav_a_color: rgb(255, 255, 255);
     $nav_a_router_link_exact_active_color: rgb(133, 186, 255);
     $nav_a_hover_color: #5f85db;
     ```

     

2. src/vue.config.js
   sass-loader v8 버전 이상부터 이 옵션을 적용할 수 있다.

   ```js
   const { defineConfig } = require('@vue/cli-service')
   module.exports = defineConfig({
     transpileDependencies: ['vuetify'],
     css: {
       loaderOptions: {
         scss: {
           additionalData: `@import "@/assets/_variabled.scss";`
         }
       }
     }
   })
   ```

   

3. 사용하기

```vue
<style lang="scss">
// @import "@/assets/_variabled.scss";
    
nav {
  padding: 1.2rem !important;
  background-color: $nav_color;
  z-index: 1;
  a {
    font-size: 1.2rem !important;
    color: $nav_a_color; 
    text-decoration: none !important;
  }

  a.router-link-exact-active {
    color: $nav_a_router_link_exact_active_color !important;
  }

  a:hover {
    color: $nav_a_hover_color !important;
  }
}
    
</style>
```





## before Sass vs after Sass

### before Sass

```vue
<style>
nav {
  background-color: white;
}

nav a {
  color: #ffffff; 
}

nav a:hover {
  color: #5f85db;
}

nav a.router-link-exact-active {
  color: #90b8f8;                     
}
</style>
```



### after Sass

```vue
<style lang="scss">
    
nav {
  background-color: $nav_color;
  a {
    color: $nav_a_color; 
  }

  a.router-link-exact-active {
    color: $nav_a_router_link_exact_active_color;
  }

  a:hover {
    color: $nav_a_hover_color;
  }
}
</style>
```

