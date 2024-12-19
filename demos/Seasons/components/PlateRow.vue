<template>
  <div class="flex flex-row h-12 divide-x-2">
    <div v-for="i in size" class="w-12 h-12 flex items-center justify-center bg-slate-300" />
  </div>
</template>

<script setup lang="ts">

defineProps<{size: number}>()
</script>