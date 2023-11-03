<template>
  <div class="drop-menu p-4" @mouseleave="hidePopper">
    <slot>
      <span class="title cursor-pointer" @click="activePopper('click')" @mouseenter="activePopper('hover')" >{{title}}</span>
      <i v-if="isMenu"></i>
    </slot>
    <transition name="fade">
      <div class="drop-menu-popper card-box flex flex-col items-center whitespace-nowrap" v-show="showPopper && isMenu">
        <div class="menu-item w-full p-2 cursor-pointer rounded-md" v-for="menu in dropMenuItems">{{menu.label}}</div>
      </div>
    </transition>
  </div>
</template>

<script setup lang="ts">
type TriggerMode = 'click' | 'hover'
type DropItem = {
  label: string
  path: string
  icon?: string
}
const props = defineProps<{
  title: string
  trigger: TriggerMode
  dropMenuItems: DropItem[]
}>()
// has drop menu
const isMenu = computed(() => {
  return Array.isArray(props.dropMenuItems) && props.dropMenuItems.length
})
const showPopper = ref<boolean>(false)
function activePopper (mode: TriggerMode) {
  const trigger = props.trigger || 'hover'
  if (trigger === mode) {
    showPopper.value = true
  }
}

function hidePopper () {
  showPopper.value = false
}
</script>

<style scoped>
.drop-menu {
  position: relative;
  .title {
    transition: color .25s;
  }
  .title:hover {
    color: var(--primary-text-color)
  }
  .drop-menu-popper {
    position: absolute;
    right: 0;
    margin-top: 10px;
    padding: 10px 20px;
    .menu-item {
      transition: background-color .3s;
    }
    .menu-item:hover {
      background-color: rgba(82, 82, 89, .32);
    }
  }
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
