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
    class="item-box border-2 border-black flex items-center justify-center text-center"
    :class="[
      size === 'large' ? 'w-32 h-32' : 'w-20 h-20',
      selected ? 'bg-gray-300' : 'bg-white',
      clickable ? 'cursor-pointer hover:bg-gray-100' : '',
    ]"
    :aria-label="`Select ${item.name}`"
    @click="handleClick"
  >
    <span class="text-sm font-medium">{{ item.name }}</span>
  </div>
</template>
