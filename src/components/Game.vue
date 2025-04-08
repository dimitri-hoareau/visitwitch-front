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

//setInterval(searchVideo, 120000);
</script>

<style scoped>
.game-item {
  display: flex;
  gap: 1rem;
  background-color: #fff;
  padding: 1rem;
  border: 1px solid #e5e5e5;
  text-align: center;
  width: 400px;
  height: 100px;
  cursor: pointer;
  border-radius: 1rem;
}

h3 {
  margin-top: 1rem;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
