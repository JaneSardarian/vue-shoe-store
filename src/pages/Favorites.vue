<script setup>
import axios from 'axios'
import { XMarkIcon } from '@heroicons/vue/24/outline'
import { onMounted, ref } from 'vue'
import CardList from '../components/CardList.vue'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(
      'https://f90c081ae671bd23.mokky.dev/favorites?_relations=items'
    )

    favorites.value = data.map((obj) => obj.item)
  } catch (error) {
    console.log(error.message)
  }
})
</script>

<template>
  <h2 class="text-lg py-2">My Favorites</h2>
  <CardList :items="favorites" is-favorites />
</template>
