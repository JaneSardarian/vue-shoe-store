<script setup>
import { HeartIcon, ShoppingBagIcon, UserIcon } from '@heroicons/vue/24/outline'
import { inject } from 'vue'
defineProps({
  totalPrice: Number
})
const { openDrawer } = inject('cart')
</script>
<template>
  <header
    class="sticky top-0 z-10 flex justify-between border-b bg-white border-zinc-100 px-10 py-8"
  >
    <router-link to="/">
      <div class="flex items-center gap-4">
        <img src="/logo.png" alt="Logo" class="w-11" />
        <div>
          <h2 class="text-xl font-bold uppercase -ml-4 -mb-1">Must Have</h2>
          <p class="text-zinc-400 -ml-4">Your perfect shoe collection</p>
        </div>
      </div>
    </router-link>

    <ul class="flex items-center gap-10">
      <li
        @click="openDrawer"
        class="flex items-center gap-2 text-zinc-500 hover:text-black cursor-pointer"
      >
        <ShoppingBagIcon class="w-6" />
        <span>$ {{ totalPrice }}</span>
      </li>
      <router-link
        to="/favorites"
        class="flex items-center gap-2 text-zinc-500 hover:text-black cursor-pointer"
      >
        <HeartIcon class="w-6" />
        <span>Favorites</span>
      </router-link>
    </ul>
  </header>
</template>
