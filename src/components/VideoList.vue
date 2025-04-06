<template>
  <div class="video-list-container">
    <div class="video-list">
      <Video v-for="video in videos" :key="video.id" :video="video" />
    </div>
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
