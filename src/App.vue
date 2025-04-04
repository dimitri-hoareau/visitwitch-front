<template>
  <div class="app">
    <Header />
    <Main />
    <Footer />
  </div>
</template>

<script setup lang="ts">
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Footer from "./components/Footer.vue";
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
</style>
