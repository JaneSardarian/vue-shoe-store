<script setup>
import { HeartIcon, PlusIcon, CheckIcon } from '@heroicons/vue/24/outline'
import { HeartIcon as HeartFill } from '@heroicons/vue/24/solid'

const props = defineProps({
  id: Number,
  image: String,
  title: String,
  price: Number,
  isFavorite: Boolean,
  isAddedToCart: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function
})
</script>
<template>
  <div
    class="relative bg-white border border-zinc-100 rounded-md p-4 hover:-translate-y-[10px] hover:shadow-lg transition duration-200"
  >
    <span @click="onClickFavorite">
      <HeartFill v-if="isFavorite" class="w-6 text-red-600 absolute top-6 right-6 cursor-pointer" />
      <HeartIcon v-else class="w-6 text-zinc-400 absolute top-6 right-6 cursor-pointer" />
    </span>

    <img :src="image" alt="shoes" />
    <p class="mt-2 text-sm uppercase">{{ title }}</p>
    <div class="flex flex-col mt-5">
      <div class="flex justify-between">
        <b>$ {{ price }}</b>
        <div>
          <span @click="onClickAdd">
            <CheckIcon v-if="isAddedToCart" class="w-6 text-green-600 cursor-pointer" />
            <PlusIcon v-else class="w-6 cursor-pointer" />
          </span>
        </div>
      </div>
    </div>
  </div>
</template>
