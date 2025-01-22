<script setup>
import { ref } from "vue";
import TodoItem from "./TodoItem.vue";

const newItem = ref("");
const todos = ref([]);

const addItem = () => {
  if (!newItem.value) {
    console.log("no input recieved");
    return;
  }
  const newTodo = {
    item: newItem.value,
    completed: false,
    id: Date.now(),
  };
  todos.value.push(newTodo);
  console.log(todos.value);
  newItem.value = "";
};

const checkOffItem = (id) => {
  const todo = todos.value.find(todo => todo.id === id);
  if (todo) {
    todo.completed = !todo.completed;
    console.log(`toggle checkoff for item ${id}`)
  }
}

const deleteItem = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id);
  console.log(`Deleted item with id ${id}`);
};
</script>

<template>
  <div
    class="flex flex-col items-center bg-gray-100 p-6 rounded-lg shadow-lg max-w-md mx-auto"
  >
    <p class="text-lg font-semibold text-gray-800 mb-4">Enter Items</p>
    <form @submit.prevent="addItem" class="flex items-center w-full mb-4">
      <input
        @click=""
        v-model="newItem"
        type="text"
        placeholder="Next item to add to list"
        class="w-full p-3 border border-gray-300 rounded-l-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
      />
      <button
        class="bg-blue-600 text-white p-3 rounded-r-lg hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50"
      >
        Add
      </button>
    </form>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :item="todo.item"
      :completed="todo.completed"
      :id="todo.id"
      @checkOff="checkOffItem"
      @deleteItem="deleteItem"
    />
  </div>
</template>
