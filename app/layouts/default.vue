<template>
  <div class="flex h-screen flex-col">
    <AppHeader />
    <main class="wrapper flex-1">
      <slot />
    </main>
    <AppFooter />
  </div>
</template>
