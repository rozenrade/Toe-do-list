<script setup lang="ts">
import { computed, ref } from 'vue'

const newTask = ref('')

// Task list
const tasks = ref([
  { text: 'Apprendre Vue.JS', done: false },
  { text: 'Apprendre TypeScript', done: false },
  { text: 'Finir le projet Pedibus', done: false },
])

//Dynamic display of task count
const taskCountMessage = computed(() =>
  tasks.value.length === 0 ? 'No tasks were added, let\'s get to work !' : 'you have ' + tasks.value.length + ' left to do!',
)

// Add a new task and increment the task count
function addTask() {
  tasks.value.push({ text: newTask.value, done: false })
  newTask.value = ''
}

function removeTask(index: number) {
  // delete FROM the index in the array
  tasks.value.splice(index, 1)
}
</script>

<template>
  <h1>Todo App</h1>
  <p>{{ taskCountMessage }}</p>
  <div>
    <ul>
      <li
        v-for="(task, index) in tasks"
        @click="task.done = !task.done"
        :class="{ active: task.done }"
      >
        {{ task.text }}

        {{ task.done ? '✔' : '✘' }}

        <!-- stop the click propagation -->
        <button @click.stop="removeTask(index)">Remove Task</button>
      </li>
    </ul>
  </div>

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
