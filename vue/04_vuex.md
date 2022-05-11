# Vue_04_Vuex





## Vuex



- Vue.js 애플리케이션에 대한 상태 관리 패턴 + 라이브러리
- 상태(state)를 전역 저장소로 관리할 수 있또록 지원하는 라이브러리
- Vue의 공식 devtools와 통합되어 기타 고급 기능을 제공
- single state tree



### 기존 prop & emit의 한계

1. 부모 자식 간의 컴포넌트 관계가 단순하면 문제가 없고, 오히려 데이터 흐름을 직관적으로 파악
2. 규모가 커지면 상태 관리가 어려워짐



### 상태 관리 패턴

- 컴포넌트의 공유된 상태를 추출하고 이를 전역에서 관리 하도록 함
- 컴포넌트 트리는 커다란 view가 되며 모든 컴포넌트는 트리에 상관없이 state(=data)에 액세스하거나 동작을 트리거
- 상태 관리 및 특정 규칙 적용과 관련된 개념을 정의하고 분리함으로써 코드의 구조와 유지 관리 기능 향상



### 핵심 컨셉



#### State

- 중앙에서 관리하는 모든 상태 정보 (data)
- 각 컴포넌트는 Vuex Store에서 state 정보를 가져와 사용
- Mutations에 의해 변경됨



#### Mutations (동기적)

- 실제로 state를 변경하는 유일한 방법
- 첫번째 인자로 항상 **state**를 받음
- Actions에서 **commit**() 메서드에 의해 호출됨



#### Actions

- 비동기 로직 작성 가능
- **context** 객체 인자를 받음 => store/index.js 파일 내에 있는 모든 요소의 속성 접근 & 메서드 호출 가능
- state를 직접 변경하지 않음
- 컴포넌트에서 **dispatch**() 메서드에 의해 호출됨



#### Getters

- state를 변경하지 않고 활용하여 계산을 수행 (computed 속성과 유사)
- 예를 들어, state에 todoList라는 해야 할 일의 목록의 경우 완료된 todo 목록만 필터링 출력하는 경우



### Todo Project

1. Create Project
   `$ vue create todo-vuex-app`

2. Add Vuex plugin in Vue CLI
   `$ vue add vuex` : store / index.js 생성 => Vuex core concepts가 작성 되는 곳

3. 컴포넌트 작성
   TodoListItem.vue, TodoList.vue, TodoForm.vue, App.vue

4. #### Create Todo

   1. state 작성 (todos 리스트 생성)

      ```js
      // index.js
      
      //...
        state: {
            todos: [
                {
                    title: '할 일1',
                    isCompleted: false,
                    date: new Date().getTime(),
                },
                {
                    title: '할 일2',
                    isCompleted: false,
                    date: new Date().getTime(),
                }
            ]
        }
      ```

      

   2. 컴포넌트에서 작성한 state에 접근

      ```vue
      // TodoList.vue
      <template>
        <div>
          <todo-list-item
            v-for="todo in $store.state.todos"
            :key="todo.date"
            :todo="todo"
          >
          </todo-list-item>
        </div>
      </template>
      
      // 위의 방법을 아래와 같이 computed로 변경
      
      <template>
        <div>
          <todo-list-item
            v-for="todo in todos"
            :key="todo.date"
            :todo="todo"
          >
          </todo-list-item>
        </div>
      </template>
      
      <scirpt>
        //...
          computed: {
            todos() {
              return this.$store.state.todos
            },
          },
      </scirpt>
      ```

      

   3. 하위 컴포넌트에서 props 받기

      ```vue
      // TodoListItem.vue
      <template>
      	<div>
              {{ todo.title }}
          </div>
      </template>
      
      
      <script>
      	//...
          props: {
              todo: Object,
          },
      </script>
      ```

      

   4. 컴포넌트에서 Action 함수 호출 : dispatch()

      ```vue
      // TodoForm.vue
      //...
          <h2>Todo Form</h2>
          <input 
            type="text"
            v-model.trim="todoTitle"
            @keyup.enter="createTodo"
          />
      
      <script>
      //...
          methods: {
          createTodo() {
            const todoItem = {
              title: this.todoTitle,
              isCompleted: false,
              date: new Date().getTime(),
            }
            if (todoItem.title) {
              this.$store.dispatch('createTodo', todoItem) // 인자1: 'action name', 인자2: object
            }
          },
        }
      </script>
      ```

   5. actions & mutations 작성

      ```js
      // index.js
      
      mutations: {
          CREATE_TODO(state, todoItem) { // 인자1: state, 인자2: object
              state.todos.push(todoItem)
          }
      },
      actions: {
          createTodo(context, todoItem) { // 인자1: context, 인자2: object
              context.commit('CREATE_TODO', todoItem) // 인자1: 'mutation name', 인자2: object
          }
      }
      
      ```

      * action의 context 객체
        Vuex store의 전반적인 맥락 속성을 모두 포함하고 있음
        context.commit으로 mutation을 호출하거나, context.state, context.getters를 통해 state와 getters에 접근 가능하고, dispatch로 다른 action도 호출 가능. 그러나 actions에서 state 조작 X

5. #### Delete Todo

   1. Delete 버튼 & 이벤트 생성 => dispatch

      ```vue
      // TodoListItem.vue
      
      <button @click="deleteTodo">
          Delete
      </button>
      
      //...
      methods: {
      	deleteTodo() {
      	this.$store.dispatch('deleteTodo', this.todo) // action 호출
      }
      }
      ```

      

   2. actions & mutations 작성

      ```js
      // index.js
      
      mutations: {
        DELETE_TODO(state, todoItem) {
            const index = state.todos.indexOf(todoItem)
            state.todos.splice(index, 1)
        },
      },
      actions: {
          deleteTodo(context, todoItem) {
              context.commit('DELETE_TODO', todoItem)
          },
      },
      ```

      * index 찾기
        indexOf 메서드를 사용하면 인자객체가 첫번째로 만나는 요소의 index를 가져옴

      

7. #### Update Todo

   1. 이벤트 작성
   
      ```vue
      // TodoListItem.vue
      <template>
        <span class="pointer" @click="updateTodoStatus">{{ todo.title }}</span>
      </template>
      
      
      <script>
      //...
          methods: {
              updateTodoStatus() {
                  this.$store.dispatch('updateTodoStatus', this.todo)
              }
          }
      </script>
      ```
   
      
   
   2. actions & mutations 작성
   
      ```js
      // index.js
      
      mutations: {
          UPDATE_TODO_STATUS(state, todoItem) {
              state.todos = state.todos.map(todo => {
                  if (todo === todoItem) {
                      todo.isCompleted = !todo.isCompleted
                  }
                  return todo
              })
          },
      },
      actions: {
          updateTodoStatus({ commit }, todoItem) {
              commit('UPDATE_TODO_STATUS', todoItem)
          },
      },
      ```
      
      
      
   3. style 작성
   
      ```vue
      <template>
        <div>
          <span 
           :class="{ 'is-completed': todo.isCompleted, 'pointer': true }"
            @click="updateTodoStatus">
              {{ todo.title }}
          </span>
        </div>
      </template>
      
      
      <style>
          .is-completed {
              text-decoration: line-through;
          }
          
          .pointer {
              cursor: pointer;
          }
      </style>
      ```
   
      
   
7. 모든, 완료한, 미완료한 Todo 개수 표시하기

   1. index.js > getters 작성
   
      ```js
      // index.js
      
      getters: {
          completedTodosCount(state) {
            return state.todos.filter(todo => {
              return todo.isCompleted === true
            }).length
          },
          notCompletedTodosCount(state) {
            return state.todos.filter(todo => {
              return todo.isCompleted === false
            }).length
          },
          todosCount(state) {
            return state.todos.length
          },
        },
      ```
   
      
   
   2. App.vue > computed 작성
   
      ```vue
      // App.vue
      <template>
        //...
          <h2>전체 Todo: {{ todosCount }}</h2>
          <h2>완료한 Todo: {{ completedTodosCount }}</h2>
          <h2>미완료 Todo: {{ notCompletedTodosCount }}</h2>
      
      <script>
      //...
          computed: {
          completedTodosCount() {
            return this.$store.getters.completedTodosCount
          },
          notCompletedTodosCount() {
            return this.$store.getters.notCompletedTodosCount
          },
          todosCount() {
            return this.$store.getters.todosCount
          },
        },
      </script>
      ```
   
      
   
   