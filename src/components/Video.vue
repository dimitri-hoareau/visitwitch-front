<template>
  <div class="video-item">
    <img :src="video.thumbnail_url" :alt="video.title" class="video-image" />
    <h3>{{ video.title }}</h3>
    <p>{{ formatDate(video.created_at) }}</p>
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
const formatDate = (dateString: string) => {
  return new Date(dateString).toLocaleString("fr-FR");
};

const goToVideo = async () => {
  window.open(props.video.url, "_blank");

  try {
    const response = await fetch("http://localhost:8000/watched-videos", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        video_id: props.video.id,
        title: props.video.title,
        url: props.video.url,
        thumbnail_url: props.video.thumbnail_url,
      }),
    });

    const result = await response.json();
    console.log("Video recorded:", result);
  } catch (error) {
    console.error("Error :", error);
  }
};
</script>

<style scoped>
.video-item {
  padding: 2rem;
  border: 1px solid black;
  text-align: center;
  margin: 1rem;
  width: 400px;
  height: 450px;
  background-color: #fff;
  border: 1px solid #e5e5e5;
  text-align: center;
  border-radius: 1rem;
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
  margin-bottom: 1rem;
}

img,
h3,
p {
  margin-bottom: 1rem;
}
</style>
