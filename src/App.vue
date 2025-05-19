<script setup lang="ts">
import { ref, type Ref } from 'vue'
import AppInventoryContainer from './components/AppInventoryContainer.vue'
import type { Item } from './types/item'
import { LEFT_ITEMS, RIGHT_ITEMS } from './configs/items'

const selectedLeft = ref(new Map())
const selectedRight = ref(new Map())

const onSelect = (
  id: number,
  selected: Ref<Map<number, Item>>,
  cells: Item[],
  condition: () => boolean,
) => {
  if (selected.value.has(id)) {
    selected.value.delete(id)
    return
  }
  if (condition()) return
  const item = cells.find((item) => item.id === id)
  if (!item) return

  selected.value.set(id, item)
}
const onSelectLeft = (id: number) => {
  onSelect(id, selectedLeft, LEFT_ITEMS, () => selectedLeft.value.size >= 6)
}
const onSelectRight = (id: number) => {
  onSelect(id, selectedRight, RIGHT_ITEMS, () => selectedRight.value.size >= 1)
}
</script>

<template>
  <AppInventoryContainer
    :left-items="LEFT_ITEMS"
    :right-items="RIGHT_ITEMS"
    :selected-left="selectedLeft"
    :selected-right="selectedRight"
    @select-left="onSelectLeft"
    @select-right="onSelectRight"
  />
</template>

<style scoped></style>
