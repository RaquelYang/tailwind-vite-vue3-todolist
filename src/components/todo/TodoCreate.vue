<script setup>
import { ref } from "vue";
const emit = defineEmits();
const todoBody = ref("");
const todoBodyInput = ref(null);
const todoCreate = () => {
  if (!todoBody.value) {
    return null;
  } else {
    emit("todoCreate", {
      body: todoBody.value,
      completed: false,
    });
    todoBody.value = "";
    todoBodyInput.value.focus();
  }
};
</script>
<template>
  <div class="flex border-b">
    <input
      @keydown.enter="todoCreate"
      ref="todoBodyInput"
      v-model="todoBody"
      class="w-full px-4 py-2 focus:outline-none"
      type="text"
    />
    <button
      @click="todoCreate"
      class="px-4 py-2 bg-indigo-500 hover:bg-indigo-600 transition ease-in-out text-white"
    >
      ADD
    </button>
  </div>
</template>
