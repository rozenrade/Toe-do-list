<script setup lang="ts">
import { ref, computed } from 'vue'

interface Task {
  text: String
  done: Boolean
  id: String
}

const tasks = ref<Task[]>([])

const tasksFromStorage = localStorage.getItem('tasks')

if (tasksFromStorage) {
  tasks.value = JSON.parse(tasksFromStorage)
}

const completedTasks = computed(() => {
  return tasks.value.filter((task) => task.done === true).length
})

const uncompletedTasks = computed(() => {
  return tasks.value.filter((task) => task.done === false).length
})

const percent = computed(() => {
  if (tasks.value.length === 0) {
    return 0
  } else {
    return Math.round((completedTasks.value / tasks.value.length) * 100)
  }
})

const totalTasks = computed(() => {
  return tasks.value.length
})
</script>

<template>
  <h1>About</h1>
  <p>The user has registered a total of {{ totalTasks }} tasks</p>
  <p>User finished {{ completedTasks }} tasks</p>
  <p>User still needs to do {{ uncompletedTasks }} tasks</p>
  <p>User is {{ percent }}% of done</p>
</template>
