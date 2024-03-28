<script setup>
import { ChevronDoubleLeftIcon } from '@heroicons/vue/24/outline'
import CartItemList from './CartItemList.vue'
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black/30 z-10"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <div class="flex items-center gap-2">
      <ChevronDoubleLeftIcon class="w-5 cursor-pointer text-zinc-400 hover:text-black transition" />
      <h2 class="text-lg uppercase">Your Bag</h2>
    </div>
    <div class="mt-10">
      <CartItemList />
      <div class="flex flex-col uppercase my-10">
        <div class="flex justify-between uppercase">
          <span class="text-md font-semibold text-zinc-900">Total</span>
          <p class="text-xl font-semibold">$ 120</p>
        </div>
        <div class="flex justify-between">
          <span class="text-md font-semibold text-zinc-900">Tax</span>
          <p class="text-xl font-semibold">$ 12</p>
        </div>
        <button
          class="mt-2 transition bg-zinc-900 text-white w-full p-2 rounded-md uppercase hover:bg-black active:bg-green-500"
        >
          Checkout
        </button>
      </div>
    </div>
  </div>
</template>
