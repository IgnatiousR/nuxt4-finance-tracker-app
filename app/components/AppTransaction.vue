<template>
  <div
    class="grid grid-cols-2 py-4 border-b border-neutral-200 dark:border-neutral-800"
  >
    <div class="flex items-center justify-between">
      <div class="flex items-center space-x-1">
        <UIcon :name="icon" :class="[iconColor]" />
        <div>{{ transaction.description }}</div>
      </div>
      <UBadge v-if="transaction.category" color="neutral" variant="outline">{{
        transaction.category
      }}</UBadge>
    </div>

    <div class="flex items-center justify-end space-x-2">
      <div>{{ currency }}</div>
      <div>
        <UDropdownMenu
          :items="items"
          :content="{
            align: 'start',
            side: 'bottom',
            sideOffset: 8,
          }"
          :ui="{
            content: 'w-48',
          }"
        >
          <UButton
            icon="lucide:ellipsis"
            color="neutral"
            variant="ghost"
            :loading="isLoading"
          />
        </UDropdownMenu>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { DropdownMenuItem } from "@nuxt/ui";
const supabaseCli = useSupabaseClient();
const toast = useToast();

const props = defineProps({
  transaction: {
    type: Object,
    default: () => ({
      id: 0,
      amount: 0,
      category: "Category",
      created_at: "2025-07-18T09:42:59.144341",
      description: "Desc",
      type: "Type",
    }),
  },
});

const isLoading = ref(false);
const deleteTransaction = async () => {
  isLoading.value = true;
  try {
    await supabaseCli
      .from("transactions")
      .delete()
      .eq("id", props.transaction.id);
    toast.add({
      title: "Transaction deleted successfully.",
      icon: "lucide:circle-check",
      color: "success",
    });
  } catch (error) {
    console.log(error);
    toast.add({
      title: "Deleted successfully.",
      icon: "lucide:circle-alert",
      color: "error",
    });
  } finally {
    isLoading.value = false;
  }
};

// const deleteTransaction = () => {
//   console.log("Pressed");
// };

const isIncome = computed(() => props.transaction.type === "Income");

const icon = computed(() =>
  isIncome.value ? "lucide:arrow-up-right" : "lucide:arrow-down-right"
);

const iconColor = computed(() =>
  isIncome.value ? "text-green-600" : "text-red-600"
);

const { currency } = useCurrency(props.transaction.amount);

const items = ref<DropdownMenuItem[]>([
  {
    label: "Edit",
    icon: "lucide:square-pen",
    onSelect() {
      console.log("Edittedd");
    },
  },
  {
    label: "Delete",
    icon: "lucide:trash-2",
    onSelect() {
      deleteTransaction();
    },
  },
]);
</script>
