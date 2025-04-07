<template>
  <div class="video-list">
    <Video v-for="video in videos" :key="video.id" :video="video" />
  </div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";
import Video from "./Video.vue";

interface VideoItem {
  id: string;
  title: string;
  created_at: string;
  url: string;
  thumbnail_url: string;
}

defineProps({
  videos: {
    type: Array as () => VideoItem[],
    default: () => [],
  },
});
</script>

<style scoped>
.video-list {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}
</style>
