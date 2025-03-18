<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 flex items-center justify-center bg-black/30"
  >
    <div
      class="bg-white rounded-lg shadow-lg w-[700px] h-[320px] pl-14 pr-14 pt-8 pb-8 relative"
    >
      <button
        @click="closeModal"
        class="absolute top-2 right-6 text-3xl text-gray-200 hover:text-gray-700 hover:cursor-pointer"
      >
        x
      </button>
      <h2 class="text-4xl font-bold mb-10">
        {{ user.name.first }} {{ user.name.last }}
      </h2>
      <div class="flex gap-12">
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

const props = defineProps(['user', 'isOpen', 'closeModal']);

const formatDate = (dateString) => {
  return new Intl.DateTimeFormat('en-GB', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',
  }).format(new Date(dateString));
};
</script>
