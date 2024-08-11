<template>
  <div
    class="bg-white flex-col w-full p-4 opacity-90 flex justify-center items-center lg:text-2xl max-w-screen-lg mx-auto"
  >
    <div style="line-height: 1.5" v-html="text"></div>
    <img v-if="first" src="/src/assets/icons/down.svg" alt="scroll-down" width="80" height="80" />
  </div>
</template>

<script setup lang="ts">
defineProps({
  text: String,
  marginBottom: String,
  first: Boolean,
});
</script>
