<template>
  <section class="main">
    <SearchBar v-model:games="games" v-model:videos="videos" />
    <GameList v-model:games="games" v-model:videos="videos" />
    <VideoList :videos="videos" />
  </section>
</template>

<script setup lang="ts">
import { ref } from "vue";
import SearchBar from "./SearchBar.vue";
import GameList from "./GameList.vue";
import VideoList from "./VideoList.vue";

const games = ref([]);
const videos = ref([]);
</script>

<style>
.main {
  background-color: #f7f7f8;
  flex: 1;
}
</style>
