<script setup lang="js"></script>
<template>
  <div class="w-[80%] text-white py-6 flex mx-auto gap-6 relative h-40">
    <img
      src="@/assets/Avatar.png"
      alt="User"
      class="w-40 absolute h-auto rounded-lg object-cover shadow-md"
    />

    <div class="ml-50 flex gap-6 items-center mt-14">
      <div>
        <h2 class="text-4xl font-bold mb-1">John Doe</h2>
        <p class="text-sm">Last online: 2 days ago</p>
      </div>

      <div class="flex gap-3 mt-2">
        <button
          class="text-[#61b8d4] bg-white hover:bg-[#70ccea] hover:text-white border border-transparent hover:border-white flex items-center gap-2 px-4 py-2 h-12 rounded-lg font-medium shadow"
        >
          <i class="fas fa-paper-plane"></i> Send Message
        </button>

        <button
          class="border border-white text-white flex items-center gap-2 px-4 py-2 h-12 rounded-lg font-medium hover:bg-white hover:text-[#70ccea] transition"
        >
          <i class="fas fa-user-plus"></i> Add Friend
        </button>
      </div>
    </div>
  </div>
</template>
