<script setup>
import Hero from './components/Body/Hero.vue';
import Table from './components/Body/Table.vue';
import Navbar from './components/Navbar.vue';
</script>

<template>
  <div class="top-0 left-0 w-screen">
    <Navbar />
  </div>

  <main class="w-screen">
    <div class="bg-[#70ccea]">
      <Hero />
    </div>
    <div>
      <Table />
    </div>
  </main>
</template>

<style scoped></style>
