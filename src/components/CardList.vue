<script setup>
import Card from './Card.vue'

defineProps({
  items: Array,
  isFavorites: Boolean
})

const emit = defineEmits(['addToFavorites', 'addToCart'])
</script>

<template>
  <div class="grid grid-cols-4 gap-5" v-auto-animate>
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :image="item.image"
      :title="item.title"
      :price="item.price"
      :onClickFavorite="isFavorites === true ? null : () => emit('addToFavorites', item)"
      :onClickAdd="isFavorites === true ? null : () => emit('addToCart', item)"
      :isFavorite="item.isFavorite"
      :isAddedToCart="item.isAddedToCart"
    />
  </div>
</template>
