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
      <TrendCom
        color="green"
        title="Income"
        :amount="4000"
        :last-amount="3000"
        :loading="false"
      />
      <TrendCom
        color="green"
        title="Income"
        :amount="4000"
        :last-amount="3000"
        :loading="true"
      />
      <TrendCom
        color="red"
        title="Income"
        :amount="4000"
        :last-amount="3000"
        :loading="false"
      />
      <TrendCom
        color="green"
        title="Income"
        :amount="4000"
        :last-amount="3000"
        :loading="false"
      />
    </section>
  </div>
</template>

<script setup>
import { transactionViewOptions } from "~/constants";
const selectedView = ref("Yearly");
</script>
