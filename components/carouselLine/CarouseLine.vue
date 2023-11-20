<template>
  <div class="carouse-line">
    <VideoCard
      class="card"
      v-for="(video, index) in videoList"
      :key="video.title"
      :style="getCardStyle(index)"
      :title="video.title"
      :cover-path="video.coverPath"
      :video-id="video.videoId"
    />
  </div>
</template>

<script setup lang="ts">
import VideoCard from "~/components/VideoCard.vue";
import type { VideoCardProps } from "~/components/types";
useHead({
  script: [{ src: "https://www.youtube.com/iframe_api" }],
});
const videoList = ref<VideoCardProps[]>([
  {
    title: "first video",
    videoId: "Yvz_axxWG4Y",
  },
  {
    title: "Animating HTML5 Canvas for Complete Beginners",
    videoId: "yq2au9EfeRQ",
  },
  {
    title: "Animating HTML5 Canvas for Complete Beginners",
    videoId: "vAJEHf92tV0",
  },
  {
    title: "HTML Canvas DEEP DIVE",
    videoId: "uCH1ta5OUHw",
  },
  {
    title: "Learn Creative Coding: Fractals",
    videoId: "dQKYao-daYw",
  },
  {
    title: "Vanilla JavaScript Pixel Rain Tutorial",
    videoId: "RCVxXgJ8xSk",
  },
  {
    title: "JavaScript 2D Game Tutorial",
    videoId: "jl29qI62XPg",
  },
]);
const basicDeg = 360 / videoList.value.length
const getCardStyle = computed(() => {
  return (index: number) => {
    return {
      // transform: `rotateY(${}deg)`
    }
  }
})
</script>

<style scoped>
.carouse-line {
  display: flex;
  flex-direction: row;
  justify-content: center;
  height: 18rem;
  position: absolute;
  gap: 1rem;
  transform-style: preserve-3d;
  .card {
    overflow: hidden;
    box-shadow: 0 1px 3px rgba(0,0,0,.5);
  }
}
.carouse-line:hover {
  animation-play-state: paused;
}
@keyframes rotateAn {
  0% {
    transform: rotateY(0);
  }
  16.7% {
    transform: rotateY(60deg);
  }
  33.3% {
    transform: rotateY(120deg);
  }
  50% {
    transform: rotateY(180deg);
  }
  66.7% {
    transform: rotateY(240deg);
  }
  83.3% {
    transform: rotateY(300deg);
  }
  100% {
    transform: rotateY(360deg);
  }
}
</style>
