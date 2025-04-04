<template>
  <form @submit.prevent="searchGame">
    <input type="text" placeholder="Search for a game" v-model="gameName" />
    <button type="submit">search</button>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue";
const gameName = ref("");
const games = ref([]);

const searchGame = async () => {
  try {
    const response = await fetch(
      `http://localhost:8000/twitch-games/${encodeURIComponent(gameName.value)}`
    );

    if (!response.ok) {
      throw new Error(`API error: ${response.status}`);
    }

    const data = await response.json();
    games.value = data;
    console.log(data);

    console.log(`Found ${data.length} games for: ${gameName.value}`);
  } catch (err) {
    console.error("Error searching for game:", err);
    games.value = [];
  }
};
</script>

<style></style>
