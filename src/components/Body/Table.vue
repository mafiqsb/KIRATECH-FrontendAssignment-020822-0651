<script setup>
import { ref, onMounted, computed } from 'vue';
import UserModal from '../UserModal.vue';

const users = ref([]);
const searchQuery = ref('');

const fetchUsers = async () => {
  try {
    const response = await fetch('https://randomuser.me/api/?results=20');
    const data = await response.json();
    users.value = data.results;
  } catch (error) {
    console.error('Error fetching users:', error);
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

const isModalOpen = ref(false);
const selectedUser = ref(null);

const openModal = (user) => {
  selectedUser.value = user;
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

// Computed property for filtering users
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
    <!-- Search Bar -->
    <div class="relative w-1/3 mb-10 ml-auto">
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

    <!-- Table Header -->
    <div
      class="flex justify-between px-6 py-3 text-gray-400 text-sm rounded-t-lg"
    >
      <span class="w-1/5">Date</span>
      <span class="w-2/5">Name</span>
      <span class="w-1/5">Gender</span>
      <span class="w-1/5">Country</span>
      <span class="w-1/5">Email</span>
    </div>

    <!-- User List -->
    <div class="space-y-3">
      <div
        v-for="(user, index) in filteredUsers"
        :key="index"
        class="flex justify-between px-6 py-4 bg-white rounded-lg shadow-md transition border border-transparent hover:cursor-pointer hover:border-[#61b8d4] hover:border-2 h-20 items-center"
        @click="openModal(user)"
      >
        <span class="w-1/5 text-gray-400 text-sm">
          {{ formatDate(user.registered.date) }}
        </span>
        <span
          class="w-2/5 text-black font-light hover:text-[#61b8d4] cursor-pointer"
        >
          {{ user.name.first }} {{ user.name.last }}
        </span>
        <span class="w-1/5 capitalize text-gray-400 text-sm font-light">{{
          user.gender
        }}</span>
        <span class="w-1/5 text-sm font-light">{{
          user.location.country
        }}</span>
        <span class="w-1/5 text-gray-400 text-sm">{{ user.email }}</span>
      </div>
    </div>

    <!-- User Modal -->
    <UserModal
      :user="selectedUser"
      :isOpen="isModalOpen"
      :closeModal="closeModal"
    />
  </div>
</template>
