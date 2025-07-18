<template>
  <div>
    <section class="flex items-center justify-between mb-10">
      <h1 class="text-4xl font-extrabold">Summary</h1>
      <div>
        <USelectMenu
          v-model="selectedView"
          :items="transactionViewOptions"
          class="w-32"
        />
      </div>
    </section>
    <section
      class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 sm:gap-16 mb-10"
    >
      <AppTrend
        color="green"
        title="Income"
        :amount="4000"
        :last-amount="3000"
        :loading="false"
      />
      <AppTrend
        color="green"
        title="Income"
        :amount="4000"
        :last-amount="3000"
        :loading="true"
      />
      <AppTrend
        color="red"
        title="Income"
        :amount="4000"
        :last-amount="7000"
        :loading="false"
      />
      <AppTrend
        color="green"
        title="Income"
        :amount="4000"
        :last-amount="3000"
        :loading="false"
      />
    </section>
    <section>
      <div
        v-for="(transactionsOnDay, date) in transactionsGroupByDate"
        :key="date"
        class="mb-10"
      >
        <AppDailyTransactionSummary
          :date="date"
          :transactions="transactionsOnDay"
        />
        <AppTransaction
          v-for="transaction in transactionsOnDay"
          :key="transaction.id"
          :transaction="transaction"
        />
      </div>
    </section>
  </div>
</template>

<script setup>
import { transactionViewOptions } from "~/constants";

const selectedView = ref("Yearly");
const supabaseCli = useSupabaseClient();
const transactions = ref([]);

const { data } = await useAsyncData("transactions", async () => {
  const { data, error } = await supabaseCli.from("transactions").select();
  if (error) return [];
  return data;
});

transactions.value = data.value;

const transactionsGroupByDate = computed(() => {
  let groupedByDate = {};

  for (const transaction of transactions.value) {
    const date = new Date(transaction.created_at).toISOString().split("T")[0];

    if (!groupedByDate[date]) {
      groupedByDate[date] = [];
    }

    groupedByDate[date].push(transaction);
    // console.log(date);
  }
  return groupedByDate;
});

console.log(transactionsGroupByDate.value);
// console.log(data);
</script>
