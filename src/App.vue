<template>
  <header>
    <nav>
      <RouterLink to="/">Calculator</RouterLink>
      <RouterLink to="/contact">Contact</RouterLink>
    </nav>
  </header>

  <RouterView />
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
</script>

<style scoped>
nav {
  padding: 4px;
  background-color: rgba(0, 0, 0, 0.5);
}

a {
  padding: 4px;
  margin: 4px;
  text-decoration: none;
  color: #f69806;
}

.router-link-active {
  color: orangered;
}
</style>
