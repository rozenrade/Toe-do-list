<script setup lang="ts">
const props = defineProps(['task'])
const emit = defineEmits(['remove', 'toggle'])
</script>

<template>
  <!-- emit allows to signal to parent giving orders -->
  <li @click="emit('toggle')" :class="{ active: task.done }">
    {{ task.text }}

    {{ task.done ? '✔' : '✘' }}
    <!-- stop the click propagation -->
    <button @click.stop="emit('remove')">Remove Task</button>
  </li>
</template>
