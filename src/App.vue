<script setup>
import Hero from './components/layout/HeroSection.vue';
import Table from './components/user/UserListTable.vue';
import Navbar from './components/layout/NavbarSection.vue';
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
