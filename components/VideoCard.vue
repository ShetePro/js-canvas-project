<template>
  <div
    ref="cardRef"
    class="video-card rounded-xl"
    :style="getTransformStyle"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
  >
    <!--    <img :src="coverImage" alt="视频封面" id="video-cover" />-->
    <div :id="videoId"></div>
    <slot></slot>
  </div>
</template>

<script setup lang="ts">
import type { VideoCardProps } from "~/components/types";
import { onMounted } from "vue";
import {width} from "@unocss/preset-mini/theme";
const props = defineProps<VideoCardProps>();
const isHover = ref<boolean>(false);
const coverImage = ref<string>(props.coverPath || "");
const player = ref();
const cardRef = ref<HTMLDivElement>();
const baseX = 5;
const baseY = 20;
const baseDeg = 5;
// const videUrl = ref<string>();
onMounted(() => {
  getYoutubeData();
  onYouTubeIframeAPIReady();
});

const getYoutubeData = async () => {
  const response: any = await fetch(
    `https://www.googleapis.com/youtube/v3/videos?id=${props.videoId}&key=AIzaSyCRoOI9u3wuz9FsOpv1RUTCPfc_aLfjiyM&part=snippet`,
  );
  const data = await response.json();
  const image = data.items[0]?.snippet?.thumbnails?.standard.url;
  if (image) {
    coverImage.value = image;
  }
};
const getTransformStyle = computed(() => {
  const box = cardRef.value?.getBoundingClientRect();
  const {left = 0, right, width = 0, height= 0} = box || {};
  const index = left > width ? Math.ceil(left / width) : 1
  const center = Math.ceil(document.body.offsetWidth / width / 2)
  const num = Math.abs(index - center);
  console.log(box?.height)
  console.log('center', center);
  if (index === center) {
    return {
      width: '35rem',
      height: '22rem',
      transform: `rotateX(0deg) rotateY(0deg) translateZ(1rem) translateY(0px)`
    }
  }else if (index > center) {
    return {
      transform: `rotateX(${num * baseDeg + baseX}deg) rotateY(${num * baseDeg + baseY}deg) translateZ(1rem) translateY(${height * num / 5}px)`
    }
  }
  return {
    transform: `rotateX(-${num * baseDeg + baseX}deg) rotateY(${num * baseDeg + baseY}deg) translateZ(1rem) translateY(${height * num / 5}px)`
  }
})
function handleMouseEnter() {
  isHover.value = true;
}
function handleMouseLeave() {
  isHover.value = false;
}

function onYouTubeIframeAPIReady() {
  player.value = new window.YT.Player(props.videoId, {
    height: "100%",
    width: "100%",
    videoId: props.videoId, // 替换为你的实际视频ID
    playerVars: {
      autoplay: 0, // 不自动播放
      controls: 0, // 不显示播放器控件
      showinfo: 0, // 不显示视频信息
      rel: 0, // 不显示相关视频
    },
    events: {
      onReady: onPlayerReady,
    },
  });
}

function onPlayerReady() {
  const cover = document.getElementById("video-cover");
  if (cover) {
    cover.addEventListener("mouseover", function () {
      player.playVideo();
      cover.style.display = "none"; // 隐藏封面图像
    });
  }
}
</script>

<style scoped>
.video-card {
  position: relative;
  width: 30rem;
  height: 18rem;
  min-width: 30rem;
  min-height: 18rem;
  overflow: hidden;
  transition: transform 1s ease;
  .cover-image {
    position: absolute;
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 1;
  }
  .hide-cover {
    opacity: 0;
    transition: opacity 0.3s ease;
  }
}
</style>
