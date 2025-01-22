<script setup>
const props = defineProps({
  item: String,
  completed: Boolean,
  id: Number,
});

const emit = defineEmits(["checkOff", "deleteItem"]);

const checkOffItem = () => {
  emit("checkOff", props.id);
};

const deleteItem = () => {
  emit("deleteItem", props.id);
};
</script>

<template>
  <div
    class="flex items-center justify-between bg-white p-4 rounded-lg shadow-md mb-4 w-full"
  >
    <button
      @click="checkOffItem"
      v-if="!completed"
      class="bg-green-500 text-white p-2 rounded-full hover:bg-green-600 focus:outline-none focus:ring-2 focus:ring-green-500"
    >
      ☐
    </button>

    <button
      @click="checkOffItem"
      v-else
      class="bg-green-500 text-white p-2 rounded-full hover:bg-green-600 focus:outline-none focus:ring-2 focus:ring-green-500"
    >
      <span>☑</span>
    </button>

    <p
      class="flex-1 text-lg text-gray-800 {{ completed ? 'line-through text-gray-500' : '' }} mx-4"
    >
      {{ item }}
    </p>
    <button
      @click="deleteItem"
      class="bg-red-500 text-white p-2 rounded-full hover:bg-red-600 focus:outline-none focus:ring-2 focus:ring-red-500"
    >
      x
    </button>
  </div>
</template>
