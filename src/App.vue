<script setup>
// import HelloWorld from './components/HelloWorld.vue';
import { ref } from 'vue';
const inputValue = ref('');
const todoList = ref([
  { text: 'vue', done: false },
  { text: 'react', done: false },
  { text: 'vercel', done: false },
]);
const handleClickButton = () => {
  // console.log(inputValue.value);
  // console.log(todoList.value);
  // todoList.value.push(inputValue.value);
  todoList.value.push({ text: inputValue.value, done: false });
  console.log(todoList.value);
};
const handleChange = (event) => {
  // console.log(event);
  const nextValue = event.target.value;
  inputValue.value = nextValue;
};
const handleClickDeleteButton = (index) => {
  todoList.value.splice(index, 1);
};
const handleClickCheck = (index) => {
  todoList[index].value.done = True;
};
</script>
<template>
  <div>{{ todoList }}</div>
  <h1>TODO LIST</h1>
  <!--
  <input :model="inputValue" placeholder="type" />
  <input v-bind:model="inputValue" placeholder="type" />
  <input :value="inputValue" placeholder="type" />
  <input v-bind:value="inputValue" placeholder="type" /> -->
  <!-- v-bind:value or v-model만 됨 -->
  <!-- v-bind:<...>는 해당 html attribute 값과 bind 하기 때문에 "value"여야만 함 (input tag의 attribute) -->
  <input v-model="inputValue" placeholder="type" />
  <!-- <input :value="inputValue" @change="handleChange" /> -->
  <button @click="handleClickButton">확인</button>
  <div class="todo-item" v-for="(todo, index) in todoList">
    <input type="checkbox" v-model="todo.done" />
    <!-- <input type="checkbox" @click="handleClickCheck(index)" /> -->
    <span :class="{ 'done-item': todo.done }">
      {{ todo.text }}
    </span>
    <div>
      <button>수정</button>
      <button @click="handleClickDeleteButton(index)">삭제</button>
    </div>
  </div>
</template>
<style scoped>
.todo-item {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  border: 1px solid gray;
}
.done-item {
  text-decoration: line-through;
}
</style>
