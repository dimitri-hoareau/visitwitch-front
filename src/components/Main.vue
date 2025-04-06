<template>
  <section class="main">
    <SearchBar v-model:games="games" />
    <GameList :games="games" />
  </section>
</template>

<script setup lang="ts">
import { ref } from "vue";
import SearchBar from "./SearchBar.vue";
import GameList from "./GameList.vue";

const games = ref([]);
</script>

<style>
.main {
  background-color: #f7f7f8;
  flex: 1;
}
</style>
