<template>
  <div class="home-view">
    <HomeHeader />
    <NuxtPage />
  </div>
</template>
<script setup lang="ts">
import HomeHeader from "~/layout/HomeHeader.vue";
</script>
<style>
@import url('style/common.css');
.home-view {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
}
</style>
