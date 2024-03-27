<!-- Это Api options -->

<!-- <script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  }
} -->
<!-- </script> -->

<!-- А это Api Composition -->
<!-- <script setup>
import { ref } from 'vue'
let count = ref(0)

function increment() {
  count.value++
} -->

<!-- // function updateCount(event) {
//   count.value = Number(event.target.value)
// } -->
<!-- </script> -->

<!-- <template>
  <h1>{{ count }}</h1>
  <button @click="increment">+</button>
  <input @keyup.ctrl.enter="increment" />
</template> -->

<!-- <script setup>
const props = defineProps({
  title: String,
  price: Number,
  isAdded: Boolean
})

console.log(props)
</script>
<template>
  <div class="product">
    <h2>{{ title }}</h2>
    <h4>{{ price }}</h4>
    <p v-if="isAdded">Added</p>
    <slot></slot>
  </div>
</template>

<style scoped>
.product {
  border: 1px solid black;
  padding: 20px;
  margin-bottom: 10px;
}
</style> -->
