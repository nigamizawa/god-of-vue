<template>
  <div class="box_input">
    <div class="todo_input_container">
      <input
        type="text"
        placeholder="+ add something"
        class="todo_input"
        v-model="todoRef"
      />
    </div>
    <div class="btn_container">
      <button class="btn" @click="addTodo">add</button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

interface Todo {
  id: number;
  task: string;
}
type TodoList = Todo[];

const todoRef = ref('');
const todoListRef = ref<TodoList>([]);

let count = 0;

// localstorageを利用するがapiを用意したい
const addTodo = () => {
  todoListRef.value.push({
    id: count,
    task: todoRef.value,
  });
  localStorage.todoList = JSON.stringify(todoListRef.value);

  todoRef.value = '';
  count += 1;
};
</script>

<style scoped>
.box_input {
  display: flex;
  align-items: center;
  margin-top: 20px;
}

.todo_input_container {
  margin-right: 8px;
}

.todo_input {
  width: 300px;
  padding: 8px;
  font-size: 18px;
  border: 1px solid #aaa;
  border-radius: 6px;
}

.btn {
  padding: 8px;
  background-color: #03a9f4;
  border-radius: 6px;
  color: #fff;
  text-align: center;
  font-size: 14px;
}
</style>
