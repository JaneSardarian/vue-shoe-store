<script setup>
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
</script>

<template>
  <div class="bg-white w-4/5 m-auto rounded-md shadow-xl mt-14">
    <Header />
    <div class="p-10">
      <h2 class="text-lg font-bold mb-8 uppercase">All Shoes</h2>
      <CardList />
    </div>
  </div>
</template>

<style scoped></style>
