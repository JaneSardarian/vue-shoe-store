<script setup>
import { ref, reactive, watch, onMounted, provide } from 'vue'
import { MagnifyingGlassIcon } from '@heroicons/vue/24/outline'
import axios from 'axios'
import debounce from 'lodash.debounce'
import { inject } from 'vue'
import CardList from '../components/CardList.vue'
import Hero from '../components/Hero.vue'
const items = ref([])

const { addToCart, removeFromCart, cart } = inject('cart')
const filters = reactive({
  searchQuery: '',
  sortBy: 'title'
})
const addToFavorites = async (item) => {
  try {
    if (!item.isFavorite) {
      item.isFavorite = true
      const { data } = await axios.post('https://f90c081ae671bd23.mokky.dev/favorites', {
        item_id: item.id
      })

      item.favoriteId = data.id
    } else {
      item.isFavorite = false
      await axios.delete(`https://f90c081ae671bd23.mokky.dev/favorites/${item.favoriteId}`)
      item.favoriteId = null
    }
  } catch (error) {
    console.log(error.message)
  }
}
const onClickAddPlus = (item) => {
  if (!item.isAddedToCart) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
}

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}
const onChangeSearchInput = debounce((event) => {
  filters.searchQuery = event.target.value
}, 500)

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get('https://f90c081ae671bd23.mokky.dev/favorites')
    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.item_id === item.id)

      if (!favorite) {
        return item
      }
      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })
  } catch (error) {
    console.log(error.message)
  }
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }
    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }
    const { data } = await axios.get('https://f90c081ae671bd23.mokky.dev/items', { params })

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      favoriteId: null,
      isAddedToCart: false
    }))
  } catch (error) {
    console.log(error.message)
  }
}
onMounted(async () => {
  const localCart = localStorage.getItem('cart')
  cart.value = localCart ? JSON.parse(localCart) : []

  await fetchItems()
  await fetchFavorites()

  items.value = items.value.map((item) => ({
    ...item,
    isAddedToCart: cart.value.some((cartItem) => cartItem.id === item.id)
  }))
})

watch(cart, () => {
  items.value = items.value.map((item) => ({
    ...item,
    isAddedToCart: false
  }))
})
watch(filters, fetchItems)
</script>

<template>
  <Hero />
  <div class="flex justify-between items-center">
    <h2 class="text-lg py-2">All Shoes</h2>
    <div class="flex gap-4">
      <select @change="onChangeSelect" class="py-2 px-3 rounded-md outline-none">
        <option value="name">Featured</option>
        <option value="price">Price, Low to High</option>
        <option value="-price">Price, High to Low</option>
      </select>

      <div class="relative">
        <MagnifyingGlassIcon class="w-5 text-zinc-400 absolute left-3 top-2.5" />
        <input
          @input="onChangeSearchInput"
          type="text"
          placeholder="Search"
          :maxlength="30"
          class="border border-zinc-100 rounded-md py-2 pl-10 pr-4 outline-none focus:border-zinc-400 transition"
        />
      </div>
    </div>
  </div>
  <div class="mt-10">
    <CardList :items="items" @add-to-favorites="addToFavorites" @add-to-cart="onClickAddPlus" />
  </div>
</template>
