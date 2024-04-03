<script setup>
defineProps({
  image: String,
  title: String,
  description: String
})
</script>

<template>
  <div class="flex flex-col items-center text-center w-72 mx-auto">
    <img :src="image" alt="Cart Empty" />
    <h2 class="mt-4 text-2xl font-medium">{{ title }}</h2>
    <p class="mt-2 text-zinc-500">{{ description }}</p>
  </div>
</template>
