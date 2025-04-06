<template>
  <div class="game-list-container">
    <div class="game-list">
      <Game
        v-for="game in games"
        :key="game.id"
        :game="game"
        @update:videos="$emit('update:videos', $event)"
        @update:games="$emit('update:games', $event)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
import Game from "./Game.vue";

interface GameItem {
  id: string;
  name: string;
  box_art_url: string;
}
interface VideoItem {
  id: string;
  title: string;
  created_at: string;
  url: string;
  thumbnail_url: string;
}

defineProps({
  games: {
    type: Array as () => GameItem[],
    default: () => [],
  },
  videos: {
    type: Array as () => VideoItem[],
    default: () => [],
  },
});

defineEmits(["update:videos", "update:games"]);
</script>
