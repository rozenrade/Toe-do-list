<script setup lang="ts">
import TodoItem from './components/TodoItem.vue'
import { ref, computed } from 'vue'

// Task list
const tasks = ref([
  { text: 'Apprendre Vue.JS', done: false },
  { text: 'Apprendre TypeScript', done: false },
  { text: 'Finir le projet Pedibus', done: false },
])

const newTask = ref('')

// Add a new task and increment the task count
function addTask() {
  tasks.value.push({ text: newTask.value, done: false })
  newTask.value = ''
}

function removeTask(index: number) {
  // delete FROM the index in the array
  tasks.value.splice(index, 1)
}

//Dynamic display of task count
const taskCountMessage = computed(() =>
  tasks.value.length === 0
    ? "No tasks were added, let's get to work !"
    : 'you have ' + tasks.value.length + ' left to do!',
)
</script>

<template>
  <h1>Todo App</h1>
  <p>{{ taskCountMessage }}</p>
  <ul>
    <!-- index key required for reactivity -->
    <TodoItem
      v-for="(task, index) in tasks"
      :task="task"
      :key="index"
      @remove="removeTask(index)"
      @toggle="task.done = !task.done"
    />

  </ul>
  <div>
    <input v-model="newTask" />

    <button @click="addTask()">Add Task</button>
  </div>
</template>

<style scoped>
li {
  list-style-type: none;
}
.active {
  color: green;
}
</style>
