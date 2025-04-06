<template>
  <div class="game-item">
    <img :src="game.box_art_url" :alt="game.name" class="game-image" />
    <div class="game-info">
      <h3>{{ game.name }}</h3>
      <p class="game-id">ID: {{ game.id }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps({
  game: {
    type: Object,
    required: true,
  },
});
</script>
