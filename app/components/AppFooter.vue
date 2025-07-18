<template>
  <footer class="border-t border-neutral-700">
    <div class="p-5 flex-center">
      {{ currentYear }} &nbsp;<UIcon name="tdesign:copyright" />&nbsp; APP. All
      Rights Reserved
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear();
</script>
