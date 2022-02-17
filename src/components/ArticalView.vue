<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ content: string[], audio_url: string }>()

const count = ref(0)
</script>

<template>
  <template class="flex justify-center mt-2">
    <audio controls>
      <source :src="audio_url" type="audio/mpeg" />
    </audio>
  </template>
  <p class="mx-5 my-10 text-lg" v-for="line in content" :key="line">{{ line }}</p>
</template>

<style scoped>
</style>
