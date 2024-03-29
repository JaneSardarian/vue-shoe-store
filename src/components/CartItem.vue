<script setup>
import { XMarkIcon } from '@heroicons/vue/24/outline'
</script>

<template>
  <div class="flex flex-col-2 border border-zinc-100 rounded-md">
    <img class="w-32 h-24" src="/pumps/shoes-1.jpg" alt="shoes" />
    <div class="flex flex-cols-2 gap-4">
      <div class="ml-4">
        <p class="text-sm uppercase mt-1 mb-5">Avenue pumps in patent leather</p>
        <p class="text-lg font-semibold">$ 120</p>
      </div>
      <span class="flex items-center">
        <XMarkIcon class="mr-2 w-5 text-zinc-400 hover:text-zinc-900 cursor-pointer transition" />
      </span>
    </div>
  </div>
</template>
