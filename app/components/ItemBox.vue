<script setup lang="ts">
import type { Item } from '~/types/item'

interface Props {
  item: Item
  selected?: boolean
  size?: 'normal' | 'large'
  clickable?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  selected: false,
  size: 'normal',
  clickable: true,
})

const emit = defineEmits<{
  click: [item: Item]
}>()

const handleClick = () => {
  if (props.clickable) {
    emit('click', props.item)
  }
}
</script>

<template>
  <div
    class="item-box"
    :class="[
      size === 'large' ? 'item-box--large' : 'item-box--normal',
      selected ? 'item-box--selected' : '',
      clickable ? 'item-box--clickable' : '',
    ]"
    :aria-label="`Select ${item.name}`"
    @click="handleClick"
  >
    <span class="item-box__label">{{ item.name }}</span>
  </div>
</template>

<style scoped lang="scss">
.item-box {
  @apply border-2 border-black flex items-center justify-center text-center bg-white;

  &--normal {
    @apply w-20 h-20;
  }

  &--large {
    @apply w-32 h-32;
  }

  &--selected {
    @apply bg-gray-300;
  }

  &--clickable {
    @apply cursor-pointer hover:bg-gray-100;
  }

  &__label {
    @apply text-sm font-medium;
  }
}
</style>
