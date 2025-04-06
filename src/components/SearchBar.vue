<template>
  <form @submit.prevent="searchGame">
    <input type="text" placeholder="Search for a game" v-model="gameName" />
    <button type="submit">search</button>
  </form>
</template>

<script setup lang="ts">
import { ref, defineEmits } from "vue";
const emit = defineEmits(["update:games"]);
const gameName = ref("");

const searchGame = async () => {
  try {
    const response = await fetch(
      `http://localhost:8000/twitch-games/${encodeURIComponent(gameName.value)}`
    );

    if (!response.ok) {
      throw new Error(`API error: ${response.status}`);
    }

    const result = await response.json();
    // console.log(result.data);
    emit("update:games", result.data);
  } catch (err) {
    console.error("Error searching for game:", err);
    emit("update:games", []);
  }
};
</script>

<style></style>
