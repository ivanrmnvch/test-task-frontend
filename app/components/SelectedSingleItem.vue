<script setup lang="ts">
import type { Item } from '~/types/item'

interface Props {
  item: Item | null
}

defineProps<Props>()
</script>

<template>
  <div class="selected-single-item">
    <ItemBox v-if="item" :item="item" size="large" :clickable="false" />
    <div v-else class="selected-single-item__placeholder">
      <span class="selected-single-item__placeholder-text">SELECTED ITEM</span>
    </div>
  </div>
</template>

<style scoped lang="scss">
.selected-single-item {
  @apply border-2 border-black p-4 min-h-[140px] flex items-center justify-center;

  &__placeholder {
    @apply w-32 h-32 border-2 border-dashed border-gray-300 flex items-center justify-center;
  }

  &__placeholder-text {
    @apply text-gray-400 text-sm;
  }
}
</style>
