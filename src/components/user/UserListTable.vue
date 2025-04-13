<script setup>
import { ref, onMounted, computed } from 'vue';
import UserModal from './UserModal.vue';

const users = ref([]);
const searchQuery = ref('');
const selectedUser = ref(null);
const isLoading = ref(false);
const isError = ref(false);

const fetchUsers = async () => {
  isLoading.value = true;
  isError.value = false;

  try {
    const response = await fetch('https://randomuser.me/api/?results=20');
    const data = await response.json();
    users.value = data.results;
    searchQuery.value = '';
  } catch (error) {
    isError.value = true;
    console.error('Error fetching users:', error);
  } finally {
    isLoading.value = false;
  }
};

const formatDate = (dateString) => {
  return new Intl.DateTimeFormat('en-GB', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',
  }).format(new Date(dateString));
};

onMounted(fetchUsers);

const openModal = (user) => {
  selectedUser.value = user;
};

const filteredUsers = computed(() => {
  if (!searchQuery.value) {
    return users.value;
  }
  return users.value.filter((user) =>
    `${user.name.first} ${user.name.last} ${user.email} ${user.location.country}`
      .toLowerCase()
      .includes(searchQuery.value.toLowerCase())
  );
});
</script>

<template>
  <div class="w-[80%] mx-auto mt-10">
    <div class="relative md:w-1/3 mb-10 ml-auto">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search users..."
        class="w-full p-3 pl-10 border border-gray-300 rounded-lg shadow-md focus:ring-2 focus:ring-[#61b8d4] focus:outline-none"
      />
      <i
        class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 text-lg fas fa-search"
      ></i>
    </div>

    <div
      class="hidden md:flex justify-between px-6 py-3 text-gray-400 text-sm rounded-t-lg"
    >
      <span class="w-1/5">Date</span>
      <span class="w-2/5">Name</span>
      <span class="w-1/5">Gender</span>
      <span class="w-1/5">Country</span>
      <span class="w-1/5">Email</span>
    </div>

    <!-- Loading State -->
    <div v-if="isLoading" class="text-center py-10 text-gray-500 text-lg">
      <i class="fa-solid fa-spinner fa-spin"></i>
    </div>

    <!-- Error State -->
    <div
      v-if="isError && !isLoading"
      class="text-center py-10 text-red-500 text-lg"
    >
      Failed to load users. Please try again.
    </div>

    <!-- Empty Search Result -->
    <div
      v-if="!isLoading && !isError && filteredUsers.length === 0"
      class="text-center py-10 text-gray-500"
    >
      No users found.
    </div>

    <div class="space-y-3">
      <div
        v-for="(user, index) in filteredUsers"
        :key="index"
        class="bg-white rounded-lg shadow-md transition border border-transparent hover:cursor-pointer hover:border-[#61b8d4] hover:border-2 p-4 md:flex md:justify-between md:items-center"
        @click="openModal(user)"
      >
        <div class="md:hidden">
          <p class="text-gray-400 text-sm">
            <strong>Date:</strong> {{ formatDate(user.registered.date) }}
          </p>
          <p class="text-black font-medium text-lg">
            {{ user.name.first }} {{ user.name.last }}
          </p>
          <p class="capitalize text-gray-500 text-sm">
            <strong>Gender:</strong> {{ user.gender }}
          </p>
          <p class="text-gray-500 text-sm">
            <strong>Country:</strong> {{ user.location.country }}
          </p>
          <p class="text-gray-400 text-sm truncate">
            <strong>Email:</strong> {{ user.email }}
          </p>
        </div>

        <div class="hidden md:flex justify-between w-full items-center h-20">
          <span class="w-1/5 text-gray-400 text-sm">
            {{ formatDate(user.registered.date) }}
          </span>
          <span
            class="w-2/5 text-black font-light hover:text-[#61b8d4] cursor-pointer"
          >
            {{ user.name.first }} {{ user.name.last }}
          </span>
          <span class="w-1/5 capitalize text-gray-400 text-sm font-light">
            {{ user.gender }}
          </span>
          <span class="w-1/5 text-sm font-light">
            {{ user.location.country }}
          </span>
          <span class="w-1/5 text-gray-400 text-sm truncate">
            {{ user.email }}
          </span>
        </div>
      </div>

      <div class="flex justify-center mt-6 mb-6">
        <button
          class="px-6 py-3 bg-[#61b8d4] text-white font-semibold rounded-lg shadow-md transition-all duration-300 ease-in-out hover:bg-[#4fa1bb] hover:shadow-lg active:scale-95 hover:cursor-pointer"
          @click="fetchUsers"
        >
          <i class="fas fa-sync-alt animate-spin-once"></i>
          Refresh
        </button>
      </div>
    </div>

    <UserModal
      :user="selectedUser"
      :isOpen="!!selectedUser"
      @closeModal="selectedUser = null"
    />
  </div>
</template>
