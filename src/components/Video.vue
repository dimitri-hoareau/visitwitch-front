<template>
  <div class="video-item">
    <img :src="video.thumbnail_url" :alt="video.title" class="video-image" />
    <h3>{{ video.title }}</h3>
  </div>
</template>

<script setup lang="ts">
defineProps({
  video: {
    type: Object,
    required: true,
  },
});
</script>
