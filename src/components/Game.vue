<template>
  <div class="game-item" @click="searchVideo">
    <img :src="game.box_art_url" :alt="game.name" class="game-image" />
    <h3>{{ game.name }}</h3>
  </div>
</template>

<script setup lang="ts">
const emit = defineEmits(["update:videos", "update:games"]);
const props = defineProps({
  game: {
    type: Object,
    required: true,
  },
});

const searchVideo = async () => {
  try {
    const response = await fetch(
      `http://localhost:8000/twitch-videos/${encodeURIComponent(
        props.game.id
      )}?max_results=true`
    );
    if (!response.ok) {
      throw new Error(`API error: ${response.status}`);
    }
    const result = await response.json();
    console.log(result.data);
    emit("update:videos", result.data);

    if (result.data && result.data.length > 0) {
      emit("update:games", []);
    }
  } catch (err) {
    console.error("Error searching for game:", err);
    emit("update:videos", []);
  }
};
</script>

<style scoped>
.game-item {
  padding: 1rem;
  border: 1px solid black;
  text-align: center;
  width: 150px;
  height: 250px;
  cursor: pointer;
}
</style>
