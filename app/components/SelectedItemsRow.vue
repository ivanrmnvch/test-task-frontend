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
  <div class="selected-items-row border-2 border-black p-4 min-h-[140px]">
    <div class="flex flex-wrap gap-2 mb-2">
      <ItemBox v-for="item in items" :key="item.id" :item="item" :clickable="false" />
    </div>
    <p class="text-sm text-gray-600">selected: {{ items.length }} / {{ maxItems }}</p>
  </div>
</template>
