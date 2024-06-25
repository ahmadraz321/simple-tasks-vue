<script setup>
import { ref } from "vue";

const showModel = ref(false);
const newTask = ref("");
const tasks = ref([]);

function getRandomLightColor() {
  const r = Math.floor(Math.random() * 128) + 128;
  const g = Math.floor(Math.random() * 128) + 128;
  const b = Math.floor(Math.random() * 128) + 128;

  const color = `rgb(${r}, ${g}, ${b})`;
  return color;
}

const handleAddTask = () => {
  tasks.value.push({
    id: tasks.value.length + 1,
    task: newTask.value,
    date: new Date().toLocaleDateString(),
    backGroundColor: getRandomLightColor(),
  });
  newTask.value = "";
  showModel.value = false;
};
</script>

<template>
  <div
    v-show="showModel"
    class="absolute w-full h-full bg-gray-400 z-10 flex items-center justify-center content-center"
  >
    <div
      class="flex relative flex-col items-center justify-center gap-2 border border-orange-400 rounded-md p-2 bg-white"
    >
      <textarea
        name="task"
        id="task"
        cols="30"
        rows="10"
        class="border-gray-600 border rounded-md p-2"
        placeholder="Add Taks here"
        v-model="newTask"
      ></textarea>
      <div
        class="flex flex-col items-center justify-center content-center gap-1 w-full ml-3"
      >
        <button
          class="w-full bg-orange-700 text-white rounded-lg py-1 px-2 mr-3"
          @click="handleAddTask"
        >
          Add New Task
        </button>
        <button
          class="bg-orange-700 w-full text-white rounded-lg py-1 px-2 mr-3"
          @click="showModel = false"
        >
          Cancel
        </button>
      </div>
    </div>
  </div>
  <header class="flex items-center content-center justify-between mt-1 p-4">
    <h1 class="text-4xl text-orange-700 ml-3">Tasks</h1>
    <button
      class="bg-orange-700 text-white rounded-lg py-1 px-2 mr-3"
      @click="showModel = true"
    >
      Add Tasks
    </button>
  </header>

  <main class="flex flex-wrap gap-9 p-2 mx-6">
    <section
      class="border rounded-md border-gray-700 p-3 shadow-md w-72 h-60"
      v-for="task in tasks" :key="task.id"
      :style="{ backgroundColor: task.backGroundColor }"
    >
      {{ task.task }}
    </section>
  </main>
</template>
