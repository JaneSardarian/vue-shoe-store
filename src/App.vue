<script setup>
import { onMounted, ref, watch, reactive } from 'vue'
import axios from 'axios'
import { MagnifyingGlassIcon } from '@heroicons/vue/24/outline'
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([])

const filters = reactive({
  searchQuery: '',
  sortBy: 'title'
})

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}
const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
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
    items.value = data
  } catch (error) {
    console.log(error.message)
  }
}

onMounted(fetchItems)

watch(filters, fetchItems)
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-md shadow-xl mt-14">
    <Header />
    <div class="p-6">
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
              class="border border-zinc-100 rounded-md py-2 pl-10 pr-4 outline-none focus:border-zinc-400 transition"
            />
          </div>
        </div>
      </div>
      <div class="mt-10">
        <CardList :items="items" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
