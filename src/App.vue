<script setup>
import { ref, watch, provide, computed } from 'vue'

import Header from './components/Header.vue'
import Drawer from './components/Drawer.vue'

// Cart start
const cart = ref([])
const drawerOpen = ref(false)

const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))
const vatPrice = computed(() => Math.round(totalPrice.value * 0.15))

const closeDrawer = () => {
  drawerOpen.value = false
}

const openDrawer = () => {
  drawerOpen.value = true
}

const addToCart = (item) => {
  cart.value.push(item)
  item.isAddedToCart = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  item.isAddedToCart = false
}

watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  {
    deep: true
  }
)

provide('cart', { cart, removeFromCart, addToCart, openDrawer, closeDrawer })
// Cart end
</script>

<template>
  <Drawer v-if="drawerOpen" :total-price="totalPrice" :vat-price="vatPrice" />
  <div class="bg-white w-4/5 m-auto rounded-md shadow-xl mt-14">
    <Header :total-price="totalPrice" @open-drawer="openDrawer" />
    <div class="p-6">
      <router-view></router-view>
    </div>
  </div>
</template>

<style scoped></style>
