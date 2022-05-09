# Vue_02_Components



## Components

1. 템플릿 (HTML) : HTML의 body 부분, 각 컴포넌트를 작성
2. 스크립트 (JavaScript) : 컴포넌트 정보, 데이터, 메서드 등 vue 인스턴스를 구성하는 대부분이 작성
3. 스타일 (CSS) : 컴포넌트의 스타일



## 컴포넌트 등록 3단계

1. 불러오기 (import)

   ```vue
   // App.vue/script
   import MyFirstComp from './components/MyFirstComp.vue'
   ```

   

2. 등록하기 (register)

   ```vue
   // App.vue/script
   export default {
   	name: 'App',
   	components: {
   	MyFirstComp
   	}
   }
   ```

   

3. 보여주기 (print)

   ```vue
   // App.vue/template
   <my-first-comp
     :my-message="myMessage"
   >
   </my-first-comp>
   
   <script>
   import MyFirstComp from './components/MyFirstComp.vue'
   
   export default {
     name: 'App',
     components: {
       MyFirstComp
     },
     data: function () {
       return {
         myMessage: "I am your father",
       }
     }
   }
   </script>
   ```

   

4. MyFirstComp.vue 작성

   ```vue
   <template>
     <div>
       <h2>{{ myMessage }}</h2>
     </div>
   </template>
   
   <script>
   export default {
     name: 'MyFirstComp',
     props: {
       myMessage: String,
     }
   }
   </script>
   ```



## Emit event

1. 하위 컴포넌트에 data 추가

   ```vue
   <script>
   // ...
       data: function () {
           return {
               childInputData: ''
           }
       }
   </script>
   ```

2. 하위 컴포넌트의 템플릿 내부 요소에 Vue data 연결 (v-model) 및 이벤트 걸어주기

   ```vue
   <template>
     <div>
       <input type="text" v-model="childInputData" @keyup.enter="childInputChange">    
     </div>
   </template>
   ```

   

3. 이벤트가 실행시킬 메서드 작성

   1. $emit의 첫번째 인자는 커스텀 이벤트명
   2. 두번째 인자는 부모 컴포넌트에서 실행하는 함수에 전달할 인자

   ```vue
   <script>
   // ...
       methods: {
           childInputChange() {
               this.$emit('child-input-change', this.childInputData)
           }
       }
   </script>
   ```

   

4. 부모 컴포넌트 템플릿에 작성된 하위 컴포넌트에 $emit 인자명의 이벤트 작성

   ```vue
   // App.vue
   
   <template>
     // ...
       <my-first-comp 
         @child-input-change="parentGetChange"
       >
       </my-first-comp>
   ```

   

5. 부모 컴포넌트에 작성한 이벤트가 실행시킬 메서드 작성

   ```vue
   <script>
   // ...
       methods: {
           parentGetChange(inputData) {
               console.log(`자식으로부터 온 메시지: ${inputData}`)
           }
       }
   </script>
   ```

   

   ### $emit

   HTML 속성은 대소문자를 구분하지 않으며 DOM 템플릿을 사용할 때 v-on에 camelCase 이벤트를 사용할 수 없다. 그러므로 이벤트 이름은 kebab-case를 권장함

   1. 첫번째 인자 : 스트링 형태의 부모 컴포넌트의 이벤트 이름
   2. 두번째 인자 : 자식 컴포넌트의 변경사항으로 부모 컴포넌트에 이벤트가 닿으면 부모 컴포넌트에서 실행되는 메서드에 전달되는 인자

   