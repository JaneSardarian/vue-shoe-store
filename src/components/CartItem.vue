<script setup>
import { XMarkIcon } from '@heroicons/vue/24/outline'

const emit = defineEmits(['on-click-remove'])

defineProps({
  id: Number,
  image: String,
  title: String,
  price: Number
})
</script>

<template>
  <div class="flex items-center gap-4 p-4 border border-zinc-100 rounded-md">
    <img class="w-24 h-20" :src="image" :alt="title" />
    <div class="flex flex-col flex-1">
      <p class="text-sm uppercase">{{ title }}</p>
      <div class="flex justify-between mt-4">
        <p class="flex-1 text-lg font-semibold">$ {{ price }}</p>
        <XMarkIcon
          @click="() => emit('on-click-remove')"
          class="w-6 text-zinc-400 hover:text-zinc-900 cursor-pointer transition"
        />
      </div>
    </div>
  </div>
</template>
