<template>
  <div class="wrapper">
    <AppInventory
      :items="leftItems"
      color="red"
      @select="emits('selectLeft', $event)"
      :selected="selectedLeft"
    >
      <template #selectedBody>
        <span class="wrapper__left-text"
          >SELECTED: {{ selectedLeft.size }} / {{ MAX_SIZE_SELECTED }}</span
        >
      </template>
    </AppInventory>
    <AppInventory
      :items="rightItems"
      color="red"
      @select="emits('selectRight', $event)"
      :selected="selectedRight"
    ></AppInventory>
  </div>
</template>

<script setup lang="ts">
interface Props {
  leftItems: Item[]
  rightItems: Item[]
  selectedLeft: Map<number, Item>
  selectedRight: Map<number, Item>
}
const MAX_SIZE_SELECTED = 6
defineProps<Props>()
const emits = defineEmits(['selectLeft', 'selectRight'])
import type { Item } from '@/types/item'
import AppInventory from './AppInventory.vue'
</script>

<style scoped>
.wrapper {
  display: flex;
  gap: 50px;
  justify-content: space-between;
  height: 100%;
}

.wrapper__left-text {
  align-self: center;
  margin-top: auto;
}
</style>
