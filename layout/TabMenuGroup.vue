<template>
  <div class="flex flex-row items-center justify-around">
    <DropdownMenu title="Project" :drop-menu-items="projectMenu"></DropdownMenu>
    <DropdownMenu title="Design"></DropdownMenu>
    <DropdownMenu title="Help"></DropdownMenu>
  </div>
</template>

<script setup lang="ts">
const projectMenu = [
  {
    label: 'basic',
    path: '/basic'
  },
  {
    label: 'intermediate',
    path: '/intermediate'
  },
  {
    label: 'advanced',
    path: '/advanced'
  },
  {
    label: 'expert',
    path: '/expert'
  },
]
</script>

<style scoped>

</style>
