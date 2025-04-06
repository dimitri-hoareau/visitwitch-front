<template>
  <div class="game-list-container">
    <div v-if="games.length === 0">
      <p>Aucun jeu trouvé. Essayez une autre recherche.</p>
    </div>
    <div v-else class="game-list">
      <Game v-for="game in games" :key="game.id" :game="game" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";
import Game from "./Game.vue";

interface GameItem {
  id: string;
  name: string;
  box_art_url: string;
}

const props = defineProps({
  games: {
    type: Array as () => GameItem[],
    default: () => [],
  },
});

console.log(props.games);
console.log("**************************");
</script>
