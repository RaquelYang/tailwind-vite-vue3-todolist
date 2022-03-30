<script setup>
import { onMounted, ref } from "vue";
import Heading1 from "../typography/Heading1.vue";
import TodoItem from "./TodoItem.vue";
import TodoCreate from "./TodoCreate.vue";
let todos = ref([]);
const save = () => {
  localStorage.setItem("tailwindtodos", JSON.stringify(todos.value));
};
const get = () => {
  const store = JSON.parse(localStorage.getItem("tailwindtodos"));
  console.log(store);
  todos.value = store || [];
};
onMounted(() => {
  get();
});
const todoCreate = (todo) => {
  todos.value = [...todos.value, todo];
  save();
};
const todoRemove = (index) => {
  todos.value.splice(index, 1);
  save();
};
const todoToggle = (index) => {
  save();
};
const todosClearCompleted = () => {
  todos.value = [
    ...todos.value.filter((todo) => {
      return !todo.completed;
    }),
  ];
  save();
};
</script>

<template>
  <div class="mx-auto">
    <div class="text-center">
      <Heading1>Just another todo app</Heading1>
    </div>
    <div class="shadow-lg mt-8 max-w-lg mx-auto">
      <TodoCreate @todoCreate="todoCreate" />
      <TodoItem
        v-for="(todo, index) in todos"
        :todo="todo"
        :index="index"
        @todoRemove="todoRemove"
        @todoToggle="todoToggle"
      ></TodoItem>
    </div>
    <div class="mt-8 max-w-lg mx-auto">
      <button
        @click="todosClearCompleted"
        class="px-8 py-2 bg-red-500 text-white hover:bg-red-600"
      >
        Clear completed
      </button>
    </div>
  </div>
</template>
