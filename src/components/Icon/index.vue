<template>
  <span>
    <Icon :icon="icon" :width="width" :height="height"/>
  </span>
</template>
<script>
import { Icon } from '@iconify/vue';
export default {
  components: {
    Icon,
  },
  props: {
    icon: {
      type: String,
      default: 'heroicons-outline:home',
    },
    width: {
      type: String,
      default: '25',
    },
    height: {
      type: String,
      default: '25',
    },
  },
};
</script>
<style lang=""></style>
