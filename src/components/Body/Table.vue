<script setup>
import { ref, onMounted } from 'vue';

const users = ref([]);

const fetchUsers = async () => {
  try {
    const response = await fetch('https://randomuser.me/api/?results=20');
    const data = await response.json();
    users.value = data.results;
  } catch (error) {
    console.error('Error fetching users:', error);
  }
};

onMounted(fetchUsers);
</script>

<template>
  <div class="w-[80%] mx-auto mt-10">
    <table class="w-full border-collapse bg-white shadow-lg rounded-lg">
      <thead>
        <tr class="text-gray-500 border-b">
          <th class="py-3 px-4 text-left">Date</th>
          <th class="py-3 px-4 text-left">Name</th>
          <th class="py-3 px-4 text-left">Gender</th>
          <th class="py-3 px-4 text-left">Country</th>
          <th class="py-3 px-4 text-left">Email</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(user, index) in users"
          :key="index"
          class="border-b hover:border-teal-400 hover:shadow-md transition duration-300"
        >
          <td class="py-4 px-4">
            {{ new Date(user.registered.date).toDateString() }}
          </td>
          <td class="py-4 px-4 text-teal-500 font-medium hover:underline">
            {{ user.name.first }} {{ user.name.last }}
          </td>
          <td class="py-4 px-4">{{ user.gender }}</td>
          <td class="py-4 px-4">{{ user.location.country }}</td>
          <td class="py-4 px-4 text-gray-500">{{ user.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
