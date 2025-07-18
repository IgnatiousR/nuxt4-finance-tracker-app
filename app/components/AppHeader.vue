<template>
  <header class="w-full border-b border-neutral-700">
    <div class="wrapper flex-between">
      <div class="flex-start">
        <NuxtLink href="/" class="flex-start">
          <!-- <img src="/public/favicon.ico" alt="logo" height="50" /> -->
          <span class="font-bold text-2xl">Finance Tracker</span>
        </NuxtLink>
      </div>
      <!-- <div class="hidden md:block">
        <div>Links</div>
      </div> -->
      <!-- <UAvatar src="https://github.com/benjamincanac.png" /> -->
      <div
        class="w-8 h-8 flex items-center justify-center text-neutral-800 rounded-full bg-neutral-200"
      >
        {{ firstInitial }}
      </div>
    </div>
  </header>
</template>

<script setup>
const firstInitial = "U";
//session.user?.name?.charAt(0).toUpperCase() ?? "U"
</script>
