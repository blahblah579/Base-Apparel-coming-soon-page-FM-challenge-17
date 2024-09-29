<template>
  <v-app>
    <v-main class="main">
      <HomePage />
    </v-main>
  </v-app>
</template>

<script setup>
import HomePage from "./components/HomePage.vue";
</script>

<style scoped>
.main {
  background-color: hsl(354, 53%, 52%);
  /* background-color: hsl(353, 100%, 98%); */
}
</style>
