<template>
  <div>
    <div class="font-bold" :class="[color]">{{ title }}</div>
    <div class="text-2xl font-extrabold text-black dark:text-white mb-2">
      <USkeleton v-if="loading" class="h-8 w-full" />
      <div v-else>{{ amount }}</div>
    </div>

    <div>
      <USkeleton v-if="loading" class="h-6 w-full" />
      <div v-else class="flex space-x-1 items-center text-sm">
        <UIcon
          name="material-symbols:trending-up"
          class="w-6 h-6"
          :class="[color]"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  amount: Number,
  lastAmount: Number,
  color: String,
  loading: Boolean,
});
</script>
