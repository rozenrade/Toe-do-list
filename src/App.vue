<script setup lang="ts">
import TodoItem from './components/TodoItem.vue'
import { ref, computed, watch } from 'vue'

// Task list
const tasks = ref([{ text: 'Ma première tâche', done: false, id: crypto.randomUUID() }])
const tasksFromStorage = localStorage.getItem('tasks')
const currentFilter = ref('all')
const newTask = ref('')

if (tasksFromStorage) {
  tasks.value = JSON.parse(tasksFromStorage)
}

// FILTERS
// if needed to access ref, .value mandatory
const taskState = computed(() => {
  if (currentFilter.value === 'done') {
    return tasks.value.filter((task) => task.done === true)
  } else if (currentFilter.value === 'active') {
    return tasks.value.filter((task) => task.done === false)
  } else {
    return tasks.value
  }
})

//Dynamic display of task count
const taskCountMessage = computed(() =>
  tasks.value.length === 0
    ? "No tasks were added, let's get to work !"
    : 'you have ' + tasks.value.length + ' left to do!',
)

// Add a new task and increment the task count
function addTask() {
  if (newTask.value === '') {
    return
  }
  tasks.value.push({ text: newTask.value, done: false, id: crypto.randomUUID() })

  newTask.value = ''
}

function removeTask(id: string) {
  // access id via value
  const index = tasks.value.findIndex((task) => task.id === id)
  tasks.value.splice(index, 1)
}

watch(
  tasks,
  () => {
    localStorage.setItem('tasks', JSON.stringify(tasks.value))
  },
  { deep: true },
)
</script>

<template>
  <h1>Todo App</h1>
  <h2>{{ taskCountMessage }}</h2>
  <div class="filter">
    <button @click="currentFilter = 'all'">Toutes</button>
    <button @click="currentFilter = 'active'">En cours</button>
    <button @click="currentFilter = 'done'">Terminées</button>
  </div>

  <div class="new-task">
    <input v-model="newTask" />

    <button @click="addTask()">Add Task</button>
  </div>

  <ul>
    <!-- index key required for reactivity -->
    <!-- Loop on computed for a dynamic rendering -->
    <TodoItem
      v-for="task in taskState"
      :task="task"
      :key="task.id"
      @remove="removeTask(task.id)"
      @toggle="task.done = !task.done"
    />
  </ul>
</template>

<style scoped>
h1 {
  font-size: 40px;
  font-weight: bold;
  font-family: Arial, Helvetica, sans-serif;
  margin-bottom: 20px;
  text-align: center;
}

h2 {
  font-size: 20px;
  font-weight: bold;
  font-family: Arial, Helvetica, sans-serif;
  margin-bottom: 20px;
  text-align: center;
}

.filter {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
  gap: 10px;
  font-size: 20px;
  font-weight: bold;
}

li {
  list-style-type: none;
  margin-bottom: 10px;
  font-size: 20px;
  font-weight: bold;
  font-family: Arial, Helvetica, sans-serif;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 10px;
  color: rgb(117, 117, 117);
}

ul {
  width: 300px;
  margin: 20px auto 0 auto;
  border: 1px solid rgba(0, 0, 0, 0.175);
  padding: 10px;
  background-color: #9090903f;
}
.active {
  color: rgb(81, 166, 81);
}

.new-task {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-bottom: 20px;
  gap: 10px;
  width: 300px;
  margin: 0 auto;
}
</style>
