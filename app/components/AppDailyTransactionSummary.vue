<template>
  <div
    class="grid grid-cols-2 py-4 border-b border-neutral-200 dark:border-neutral-800 text-neutral-500 dark:text-neutral-400"
  >
    <div class="flex items-center justify-between">
      {{ date }}
    </div>

    <div class="flex items-center justify-end mr-10">{{ currency }}</div>
  </div>
</template>

<script setup>
const props = defineProps({
  date: {
    type: String,
    default: "",
  },
  transactions: {
    type: Array,
    default: () => [],
  },
});

const sum = computed(() => {
  let sum = 0;

  for (const transaction of props.transactions) {
    if (transaction.type === "Income") sum += transaction.amount;
    else sum -= transaction.amount;
  }

  return sum;
});

const { currency } = useCurrency(sum);
</script>
