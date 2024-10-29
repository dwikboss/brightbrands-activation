<template>
  <RouterView />
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({});
</script>

<style lang="scss">
#app {
  height: 100vh;
  overflow: hidden;
  background-color: #ffff2b;
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.page {
  min-height: 100vh;
  height: 100%;
}
</style>
