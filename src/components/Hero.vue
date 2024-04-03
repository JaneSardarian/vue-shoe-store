<script setup>
import hero from '../../public/pumps/hero.png'
</script>

<template>
  <div
    class="w-full h-96 bg-no-repeat bg-cover bg-center mb-10 relative"
    :style="`background-image: url('${hero}');`"
  ></div>
  <div class="absolute top-1/2 left-2/3 -translate-x-1/2 -translate-y-1/2">
    <h1 class="text-5xl uppercase">Summer 24</h1>
  </div>
</template>
