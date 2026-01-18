<script setup lang="ts">
import type { Item } from '~/types/item'

interface Props {
  items: Item[]
  selectedIds: number[]
  disabled?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  disabled: false,
})

const emit = defineEmits<{
  select: [item: Item]
}>()

const isSelected = (id: number) => props.selectedIds.includes(id)

const handleSelect = (item: Item) => {
  emit('select', item)
}
</script>

<template>
  <div class="items-list" :class="{ 'items-list--disabled': disabled }">
    <div class="items-list__grid">
      <ItemBox
        v-for="item in items"
        :key="item.id"
        :item="item"
        :selected="isSelected(item.id)"
        :clickable="!disabled || isSelected(item.id)"
        @click="handleSelect"
      />
    </div>
  </div>
</template>

<style scoped lang="scss">
.items-list {
  @apply border-2 border-black p-4 min-h-[300px];

  &--disabled {
    @apply opacity-70;
  }

  &__grid {
    @apply grid grid-cols-4 gap-2;
  }
}
</style>
