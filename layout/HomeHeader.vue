<template>
  <header class="home-header flex flex-col m-2">
    <div class="content">
      <div class="flex h-full flex-row items-center">JsCanvasProject</div>
      <div class="flex flex-row">
        <TabMenuGroup />
      </div>
    </div>
  </header>
</template>

<script setup lang="ts">

import TabMenuGroup from "~/layout/TabMenuGroup.vue";
</script>

<style scoped>
.home-header {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  z-index: 30;
  display: flex;
  flex-direction: row;
  justify-content: center;
  .content {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 0 32px;
    height: 64px;
    width: 100%;
    max-width: calc(var(--layout-max-width) - 64px);
  }
}
</style>
