<script setup lang="ts">
import { userItems, choiceItems } from '~/data/items'
import { useSelectionStore } from '~/stores/selection'

const store = useSelectionStore()
</script>

<template>
  <div class="page">
    <!-- Верхняя часть: выбранные вещи -->
    <section class="page__top">
      <SelectedItemsRow :items="store.selectedUserItems" :max-items="6" />
      <SelectedSingleItem :item="store.selectedChoiceItem" />
    </section>

    <!-- Нижняя часть: списки вещей -->
    <section class="page__bottom">
      <ItemsList
        :items="userItems"
        :selected-ids="store.selectedUserItems.map((i) => i.id)"
        :disabled="!store.canAddMoreUserItems"
        @select="store.toggleUserItem"
      />
      <ItemsList
        :items="choiceItems"
        :selected-ids="store.selectedChoiceItem ? [store.selectedChoiceItem.id] : []"
        @select="store.toggleChoiceItem"
      />
    </section>
  </div>
</template>

<style scoped lang="scss">
.page {
  @apply max-w-4xl mx-auto p-4;

  &__top {
    @apply grid grid-cols-2 gap-4 mb-4;
  }

  &__bottom {
    @apply grid grid-cols-2 gap-4;
  }
}
</style>
