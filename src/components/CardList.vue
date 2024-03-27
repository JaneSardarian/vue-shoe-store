<script setup>
import Card from './Card.vue'
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      image-url="/sneakers/sneakers-1.jpg"
      title="Sneakers"
      :price="120"
      :is-added-to-cart="true"
      :is-favorite="true"
      :on-click-add="
        () => {
          console.log('added')
        }
      "
    />
  </div>
</template>
