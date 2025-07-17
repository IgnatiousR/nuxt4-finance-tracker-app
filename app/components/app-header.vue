<template>
  <header class="w-full border-b border-neutral-700">
    <div class="wrapper flex-between">
      <div class="flex-start">
        <NuxtLink href="/" class="flex-start ml-4">
          <!-- <img src="/public/favicon.ico" alt="logo" height="50" /> -->
          <span class="hidden lg:block font-bold text-2xl ml-3"> AppName </span>
        </NuxtLink>
      </div>
      <div class="hidden md:block">
        <div>Links</div>
      </div>
      <UAvatar src="https://github.com/benjamincanac.png" />
    </div>
  </header>
</template>
