<template>
  <div
    v-if="isOpen"
    class="fixed z-[6] inset-0 flex items-center justify-center bg-black/30"
    @click="closeModal"
  >
    <div
      class="bg-white rounded-lg shadow-lg w-[90%] max-w-[700px] h-auto sm:w-[90%] sm:h-auto sm:px-6 sm:py-6 pl-14 pr-14 pt-8 pb-8 relative"
      @click.stop
    >
      <button
        @click="closeModal"
        class="absolute top-4 right-6 text-3xl text-gray-200 hover:text-gray-700 hover:cursor-pointer"
      >
        <i class="fa-solid fa-xmark"></i>
      </button>
      <h2 class="text-4xl font-bold mb-10">
        {{ user.name.first }} {{ user.name.last }}
      </h2>
      <div class="flex gap-2 md:gap-12 overflow-x-auto whitespace-nowrap">
        <div class="space-y-2">
          <p>
            <strong class="text-gray-300 font-light">Date:</strong>
          </p>
          <p>
            <strong class="text-gray-300 font-light">Status:</strong>
          </p>
          <p>
            <strong class="text-gray-300 font-light">Gender:</strong>
          </p>
          <p>
            <strong class="text-gray-300 font-light">Country:</strong>
          </p>
          <p>
            <strong class="text-gray-300 font-light">Email:</strong>
          </p>
        </div>
        <div class="space-y-2">
          <p class="text-gray-900 font-light">
            {{ formatDate(user.registered.date) }}
          </p>

          <p class="text-gray-900 font-light">
            {{ user.status === 'active' ? 'Active' : 'Inactive' }}
          </p>
          <p class="text-gray-900 font-light">
            {{ user.gender }}
          </p>
          <p class="text-gray-900 font-light">
            {{ user.location.country }}
          </p>
          <p class="text-gray-900 font-light">
            {{ user.email }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  user: Object,
  isOpen: Boolean,
});
const emits = defineEmits(['closeModal']);

const closeModal = () => {
  emits('closeModal');
};

const formatDate = (dateString) => {
  return new Intl.DateTimeFormat('en-GB', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',
  }).format(new Date(dateString));
};
</script>
