<script setup>
import { inject, ref, computed } from 'vue'
import axios from 'axios'
import { ChevronDoubleLeftIcon, XMarkIcon } from '@heroicons/vue/24/outline'
import CartItemList from './CartItemList.vue'
import InfoBlock from './InfoBlock.vue'

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number
})

const { cart, closeDrawer } = inject('cart')

const isCreating = ref(false)
const orderId = ref(null)
const createOrder = async () => {
  try {
    isCreating.value = true
    const { data } = await axios.post('https://f90c081ae671bd23.mokky.dev/orders', {
      items: cart.value,
      totalPrice: props.totalPrice.value
    })

    cart.value = []

    orderId.value = data.id
  } catch (error) {
    console.log(error.message)
  } finally {
    isCreating.value = false
  }
}

const cartIsEmpty = computed(() => cart.value.length === 0)
const buttonDisabled = computed(() => isCreating.value || cartIsEmpty.value)
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black/30 z-10"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <div class="flex items-center gap-2">
      <ChevronDoubleLeftIcon
        class="w-5 cursor-pointer text-zinc-400 hover:text-black transition"
        @click="closeDrawer"
      />

      <h2 class="text-lg uppercase">Your Bag</h2>
    </div>
    <div class="mt-10">
      <div v-if="!totalPrice || orderId" class="flex h-full items-center">
        <InfoBlock
          v-if="!totalPrice && !orderId"
          title="Your cart is empty"
          image="/empty-cart.png"
        />
        <InfoBlock
          v-if="orderId"
          title="Thank you for your order!"
          image="/order-success.png"
          :description="`Order No. ${orderId} has been created. Check your email for details`"
        />
      </div>

      <div v-else>
        <CartItemList />

        <div class="flex flex-col uppercase my-8">
          <div class="flex justify-between uppercase items-center">
            <span class="text-sm font-semibold text-zinc-900">Total</span>
            <p class="text-xl font-semibold">$ {{ totalPrice }}</p>
          </div>
          <div class="flex justify-between items-center">
            <span class="text-sm font-semibold text-zinc-900">Tax 20%</span>
            <p class="text-xl font-semibold">$ {{ vatPrice }}</p>
          </div>
          <button
            :disabled="buttonDisabled"
            @click="createOrder"
            class="mt-2 transition bg-cyan-400 disabled:bg-zinc-400 text-white w-full p-2 rounded-md uppercase hover:bg-cyan-500 active:bg-green-500"
          >
            Checkout
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
