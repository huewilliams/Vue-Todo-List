<template>
  <div id="app">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <!-- @removeTodo : v-on:removeTodo 의 약식 문법 -->
      <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
      <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader'
import TodoInput from './components/TodoInput'
import TodoList from './components/TodoList'
import TodoFooter from './components/TodoFooter'

export default {
  data() {
    return {
      todoItems: []
    }
  },
  methods: {
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      // splice : 특정 인덱스부터 지정된 수 만큼 배열에서 삭제하는 API
      this.todoItems.splice(index, 1);
    }
  }
  ,
  components: {
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  },
  created() {
    if (localStorage.length > 0) {
      for(let i=0; i<localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i))
      }
    }
  }
}
</script>

<style>
  body {
    text-align : center;
    background-color : #F6F6F8
  }
  input {
    border-style : groove;
    width: 200px;
  }
  button {
    border-style : groove;
  }
  .shadow {
    box-shadow : 5px 10px 10px rgba(0,0,0,0.03)
  }
</style>
