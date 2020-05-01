<template>
  <div id="app">
    <div class="container">
      <div class="col-md-9 offset-md-3">
        <h1 class="text-center mb-4">Todo 어플리케이션</h1>
                                                            <!-- 엔터키를 누르면 addNewTodo 메소드 호출 -->
        <input type="text" class="form-control mb-4" v-model="userInput" @keyup.enter="addNewTodo">
 
        <div class="list-group mb-4">
          <!-- 버튼을 이용해 입력한 todoList만큼 생성: v-for이용, v-for만 사용할 시 에러가 발생하므로 v-bind:key를 추가해주어야 함 -->
          <!-- @click의 toggleTodoState의 todo는 v-for에서 넘겨받는 todo임 : 헷갈릴 경우 template으로 분리하여 작성 -->
          <template v-for="todo in activeTodoList"><!-- 변수처럼 사용 가능 -->
          <!-- 출력할 label값을 넣어주고, component내부에서 발생시킨 componentClick이라는 이벤트를 받아 toggleTodostate 메소드 호출 -->
              <todo v-bind:key="todo"
                  :label="todo.label" 
                  @componentClick="toggleTodoState(todo)"
              />
          </template>
        </div>

        <div class="text-right">
          <button type="button" class="btn btn-sm" @click="chanageCurrentState('active')">할 일</button>
          <button type="button" class="btn btn-sm" @click="chanageCurrentState('done')">완 료</button>
          <button type="button" class="btn btn-sm" @click="chanageCurrentState('all')">전 체</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// component에 생성한 vue파일 import
import todo from './components/todo';

export default {
  name: 'app',
  data(){
    return{
      userInput: '',
      todoList: [],
      currentState: 'active'
    };
  },
  computed:{
    // 메소드라는 것은 단순히 값을 가져오기 보다는 메소드 호출 시 내부 값을 변경하거나 ajax로 외부에서 값을 읽어온다고 하는 등의 내부 상태값을 변경시키는 용도로 사용하는 것이 일반적이므로
    // 해당 코드를 methods로 만드는 것 보다는json객체인 coumputed로 만드는 것이 나음
    // computed는 클래스의 getter함수처럼 동작함
    activeTodoList(){
      // state값이 active인 항목만 넘겨주도록 filter()추가
      // -> currentState값이 all인 경우 모든 항목을 다 가져오고 아닐 경우 currentState값과 동일한 항목만 가져오도록 fillter()의 내용을 변경해줌 
      return this.todoList.filter(todo => this.currentState === 'all' || todo.state === this.currentState);
    }
  },
  methods:{
    addNewTodo(){
        this.todoList.push({
          label: this.userInput, // 사용자가 입력한 값을 todoList에 추가
          state: 'active' // todoList의 상태값 추가: state가 active이면 완료하지 않은 항목, 클릭 시 done으로 변경하여 완료한 항목으로 표시
        }); 
        this.userInput = ''; // 추가 후 userInput 초기화시켜줌
    },
    toggleTodoState(todo){ // 버튼 클릭 시 state값을 변경할 메소드, todo:클릭한 항목을 받을 변수
        todo.state = todo.state === 'active' ? 'done' : 'active'; // 넘겨받은 todo json객체의 state값을 done과 active로 번갈아가며 설정해주도록 함
    },
    chanageCurrentState(state){
      this.currentState = state;
    }
  },
  components: {
    todo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
