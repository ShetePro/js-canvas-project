<template>
  <div class="home-view">
    <HomeHeader />
    <main class="view-body">
      <NuxtPage />
    </main>
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
  align-items: center;
  width: 100%;
  height: 100%;
  .view-body {
    margin-top: 64px;
    width: 100%;
    flex-grow: 1;
  }
}
</style>
