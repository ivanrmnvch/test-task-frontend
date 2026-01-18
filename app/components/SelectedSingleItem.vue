<script setup lang="ts">
import type { Item } from '~/types/item'

interface Props {
  item: Item | null
}

defineProps<Props>()
</script>

<template>
  <div
    class="selected-single-item border-2 border-black p-4 min-h-[140px] flex items-center justify-center"
  >
    <ItemBox v-if="item" :item="item" size="large" :clickable="false" />
    <div
      v-else
      class="w-32 h-32 border-2 border-dashed border-gray-300 flex items-center justify-center"
    >
      <span class="text-gray-400 text-sm">SELECTED ITEM</span>
    </div>
  </div>
</template>
