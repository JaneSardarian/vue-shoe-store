<script setup>
import { HeartIcon, ShoppingBagIcon, UserIcon } from '@heroicons/vue/24/outline'
</script>
<template>
  <header class="flex justify-between border-b border-slate-100 px-10 py-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-xl font-bold uppercase">Sneakers</h2>
        <p class="text-slate-400">The best sneakers store</p>
      </div>
    </div>

    <ul class="flex items-center gap-10">
      <li class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
        <ShoppingBagIcon class="w-6" />
        <span>$ 120</span>
      </li>
      <li class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
        <HeartIcon class="w-6" />
        <span>Favorites</span>
      </li>
      <li class="flex items-center gap-2 text-gray-500 hover:text-black cursor-pointer">
        <UserIcon class="w-6" />
        <span>Profile</span>
      </li>
    </ul>
  </header>
</template>
