<template>
  <div class="inputBox shadow">
    <!-- v-on:keyup.enter 엔터 키를 누르는 이벤트 -->
    <input type="text" v-model="newTodoItem" placeholder="해야하는 일을 입력하세요" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>
  </div>
</template>

<script>
    export default {
        data() {
          return {
            newTodoItem : ''
          }
        },
      methods: {
          addTodo() {
            if(this.newTodoItem !== '')
            {
              // 입력값의 공백 제거
              let value = this.newTodoItem && this.newTodoItem.trim();
              this.$emit('addTodo', value);
              // 인풋 박스의 입력값 초기화
              this.clearInput();
            }
          },
        clearInput() {
            this.newTodoItem = '';
        }
      }
    }
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius : 5px;
  }
  .inputBox input {
    border-style : none;
    font-size: 0.9rem;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478Fb, #8763FB);
    display: block;
    width : 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
</style>
