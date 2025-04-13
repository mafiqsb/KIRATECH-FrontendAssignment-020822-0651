<script setup lang="js"></script>

<template>
  <div
    class="w-[90%] md:w-[80%] text-white py-6 flex flex-col md:flex-row mx-auto gap-6 relative h-auto md:h-40"
  >
    <img
      src="@/assets/Avatar.png"
      alt="User"
      class="w-24 md:w-40 h-auto rounded-lg object-cover shadow-md mx-auto md:mx-0 md:absolute"
    />

    <div
      class="md:mt-14 md:ml-52 flex flex-col md:flex-row gap-2 md:gap-6 items-center md:items-start text-center md:text-left"
    >
      <div>
        <h2 class="text-2xl md:text-4xl font-bold mb-1">John Doe</h2>
        <p class="text-sm">Last online: 2 days ago</p>
      </div>

      <div class="flex flex-col md:flex-row gap-3 mt-2">
        <button
          class="text-[#61b8d4] bg-white hover:bg-[#70ccea] hover:text-white border border-transparent hover:border-white flex items-center justify-center gap-2 px-4 py-2 h-12 rounded-lg font-medium shadow"
        >
          <i class="fas fa-paper-plane"></i> Send Message
        </button>

        <button
          class="border border-white text-white flex items-center justify-center gap-2 px-4 py-2 h-12 rounded-lg font-medium hover:bg-white hover:text-[#70ccea] transition"
        >
          <i class="fas fa-user-plus"></i> Add Friend
        </button>
      </div>
    </div>
  </div>
</template>
