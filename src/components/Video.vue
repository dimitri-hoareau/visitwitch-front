<template>
  <div class="video-item">
    <img :src="video.thumbnail_url" :alt="video.title" class="video-image" />
    <h3>{{ video.title }}</h3>
    <p>{{ video.created_at }}</p>
    <button @click="goToVideo" class="video-button">Voir la vidéo</button>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  video: {
    type: Object,
    required: true,
  },
});

const goToVideo = () => {
  window.open(props.video.url, "_blank");
};
</script>

<style scoped>
.video-item {
  padding: 1rem;
  border: 1px solid black;
  text-align: center;
  cursor: pointer;
  margin: 1rem;
  width: 400px;
  height: 450px;
}

.video-button {
  margin-top: auto;
  padding: 0.5rem 1rem;
  background-color: #5c16c5;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}

.video-button:hover {
  background-color: #772ce8;
}

.video-image {
  width: 100%;
  height: auto;
  object-fit: cover;
}
</style>
