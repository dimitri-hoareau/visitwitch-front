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

<style scoped>
form {
  margin: 1rem;
  text-align: center;
}
input {
  width: 60%;
  padding: 0.5rem;
  margin-right: 0.5rem;
  border-radius: 0.25rem;
  border: 1px solid #e5e5e5;
}

button {
  background-color: #5c16c5;
  color: #fff;
  padding: 0.5rem;
  border-radius: 0.5rem;
  border: none;
}
</style>
