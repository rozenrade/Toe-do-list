<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>
<template>
  <!-- <p><strong>Current route path:</strong> {{ $route.fullPath }}</p> -->
  <nav>
    <RouterLink to="/">Go to Home</RouterLink>
    <RouterLink to="/about">Go to About</RouterLink>
  </nav>
  <main>
    <RouterView />
  </main>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
  background-color: #f5f5f5;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  border-bottom: 1px solid #ddd;
  font-size: 18px;
  font-weight: bold;
  color: #2c3e50;
  margin-bottom: 60px;

}
</style>