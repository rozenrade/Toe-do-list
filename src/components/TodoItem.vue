<script setup lang="ts">
const props = defineProps(['task'])
const emit = defineEmits(['remove', 'toggle'])
</script>

<template>
  <!-- emit allows to signal to parent giving orders -->
  <li @click="emit('toggle')" :class="{ active: task.done }">
    <button @click.stop="emit('remove')">X</button>
    {{ task.text }}

    {{ task.done ? '✔' : '✘' }}
    <!-- stop the click propagation -->
  </li>
</template>
