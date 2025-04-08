<template>
  <form @submit.prevent="searchGame">
    <input type="text" placeholder="Search for a game" v-model="gameName" />
    <button type="submit">search</button>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue";
const emit = defineEmits(["update:videos", "update:games"]);
const gameName = ref("");

const searchGame = async () => {
  emit("update:videos", []);
  try {
    const response = await fetch(
      `http://localhost:8000/twitch-games/${encodeURIComponent(
        gameName.value
      )}?max_results=true`
    );

    if (!response.ok) {
      throw new Error(`API error: ${response.status}`);
    }

    const result = await response.json();
    emit("update:games", result.data);
    gameName.value = "";
  } catch (err) {
    console.error("Error searching for game:", err);
    emit("update:games", []);
  }
};
</script>

<style></style>
