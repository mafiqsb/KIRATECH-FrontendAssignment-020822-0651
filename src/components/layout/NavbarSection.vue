<template>
  <div class="w-[80%] md:w-[80%] mx-auto">
    <div class="text-black pt-4 pb-4 flex justify-between">
      <div class="flex">
        <img src="@/assets/Logo.png" alt="Logo" class="h-14 w-auto" />
      </div>

      <button @click="toggleMenu" class="md:hidden text-white text-2xl">
        <i :class="menuOpen ? 'fas fa-times' : 'fas fa-bars'"></i>
      </button>

      <div class="hidden md:flex gap-8 items-center">
        <button class="hover:text-gray-300" title="Notifications">
          <i class="fa fa-bell"></i>
        </button>
        <button class="hover:text-gray-300" title="Settings">
          <i class="fa fa-cog"></i>
        </button>
        <button class="hover:text-red-500" title="Logout">
          <i class="fa fa-sign-out-alt"></i>
        </button>
      </div>
    </div>
  </div>
  <div
    v-if="menuOpen"
    class="md:hidden bg-gray-700 text-white p-4 flex flex-col items-center gap-4"
  >
    <div class="flex gap-4">
      <button class="hover:text-gray-300" title="Notifications">
        <i class="fas fa-bell"></i>
      </button>
      <button class="hover:text-gray-300" title="Settings">
        <i class="fas fa-cog"></i>
      </button>
      <button class="hover:text-red-500" title="Logout">
        <i class="fas fa-sign-out-alt"></i>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Mobile menu state
const menuOpen = ref(false);
const toggleMenu = () => {
  menuOpen.value = !menuOpen.value;
};
</script>

<style scoped>
button {
  font-size: 1.25rem;
}
</style>
