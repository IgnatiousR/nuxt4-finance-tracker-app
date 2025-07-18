<script setup>
const props = defineProps({
  title: {
    type: String,
    default: "Title",
  },
  amount: {
    type: Number,
    default: 0,
  },
  lastAmount: {
    type: Number,
    default: 0,
  },
  color: {
    type: String,
    default: "green",
  },
  loading: Boolean,
});

const trendingUp = computed(() => props.amount >= props.lastAmount);
const icon = computed(() =>
  trendingUp.value ? "lucide:trending-up" : "lucide:trending-down"
);

const percentageTrend = computed(() => {
  if (props.amount == 0 || props.lastAmount == 0) return "%";
  const biggerVal = Math.max(props.amount, props.lastAmount);
  const smallerVal = Math.min(props.amount, props.lastAmount);

  const ratio = ((biggerVal - smallerVal) / smallerVal) * 100;
  return `${Math.ceil(ratio)}`;
});
</script>

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
          :name="icon"
          class="w-6 h-6"
          :class="{ green: trendingUp, red: !trendingUp }"
        />
        <div class="text-neutral-500 dark:text-neutral-400">
          {{ percentageTrend }}% vs last period
        </div>
      </div>
    </div>
  </div>
</template>
