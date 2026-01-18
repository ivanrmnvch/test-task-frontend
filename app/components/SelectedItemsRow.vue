<script setup lang="ts">
import type { Item } from '~/types/item'

interface Props {
  items: Item[]
  maxItems?: number
}

withDefaults(defineProps<Props>(), {
  maxItems: 6,
})
</script>

<template>
  <div class="selected-items-row">
    <div class="selected-items-row__items">
      <ItemBox v-for="item in items" :key="item.id" :item="item" :clickable="false" />
    </div>
    <p class="selected-items-row__counter">selected: {{ items.length }} / {{ maxItems }}</p>
  </div>
</template>

<style scoped lang="scss">
.selected-items-row {
  @apply border-2 border-black p-4 min-h-[140px];

  &__items {
    @apply flex flex-wrap gap-2 mb-2;
  }

  &__counter {
    @apply text-sm text-gray-600;
  }
}
</style>
