<script setup lang="ts">
import { userItems, choiceItems } from '~/data/items'
import { useSelectionStore } from '~/stores/selection'

const store = useSelectionStore()
</script>

<template>
  <div class="page">
    <h1 class="page__title">Тестовое задание VueJS</h1>

    <!-- Верхняя часть: выбранные вещи -->
    <section class="page__top">
      <SelectedItemsRow
        :items="store.selectedUserItems"
        :max-items="6"
        @remove="store.toggleUserItem"
      />
      <SelectedSingleItem :item="store.selectedChoiceItem" @remove="store.toggleChoiceItem" />
    </section>

    <!-- Нижняя часть: списки вещей -->
    <section class="page__bottom">
      <div class="page__list-wrapper">
        <h2 class="page__list-title">Вещи пользователя</h2>
        <ItemsList
          :items="userItems"
          :selected-ids="store.selectedUserItems.map((i) => i.id)"
          :disabled="!store.canAddMoreUserItems"
          @select="store.toggleUserItem"
        />
      </div>
      <div class="page__list-wrapper">
        <h2 class="page__list-title">Вещи на выбор</h2>
        <ItemsList
          :items="choiceItems"
          :selected-ids="store.selectedChoiceItem ? [store.selectedChoiceItem.id] : []"
          @select="store.toggleChoiceItem"
        />
      </div>
    </section>
  </div>
</template>

<style scoped lang="scss">
.page {
  @apply max-w-4xl mx-auto p-4;

  &__title {
    @apply text-2xl font-bold text-center mb-6;
  }

  &__top {
    @apply grid grid-cols-1 md:grid-cols-2 gap-4 mb-4;
  }

  &__bottom {
    @apply grid grid-cols-1 md:grid-cols-2 gap-4;
  }

  &__list-wrapper {
    @apply flex flex-col;
  }

  &__list-title {
    @apply text-sm font-medium text-gray-600 mb-2;
  }
}
</style>
