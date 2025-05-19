<template>
  <div class="inventory">
    <div class="inventory__selected">
      <div class="inventory__selected-grid" v-if="selected.size">
        <div
          class="cell"
          v-for="[key, value] in selected.entries()"
          :key="key"
          @click="onSelect(key)"
        >
          {{ value.name }}
        </div>
      </div>
      <slot name="selectedBody">
        <div class="inventory__selected-text" v-if="selected.size === 0">SELECTED ITEM</div>
      </slot>
    </div>
    <div class="inventory__body">
      <div
        class="cell"
        v-for="item in items"
        :key="item.id"
        @click="onSelect(item.id)"
        :class="{ selected: selected.get(item.id) }"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Item } from '@/types/item'

interface Props {
  items: Item[]
  color: string
  selected: Map<number, Item>
}
defineProps<Props>()
const emits = defineEmits(['select'])
const onSelect = (id: number) => {
  emits('select', id)
}
</script>

<style scoped>
.inventory {
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 30px;
}
.inventory__selected {
  height: 30%;
  border-width: 2px;
  border-style: solid;
  border-color: v-bind(color);
  width: 50%;
  padding: 15px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}
.inventory__selected-text {
  align-self: center;
}
.inventory__selected-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(60px, 1fr));
  grid-template-rows: repeat(auto-fill, 60px);
  gap: 15px;
}
.inventory__selected-text {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.inventory__body {
  border-width: 2px;
  border-style: solid;
  border-color: v-bind(color);
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  grid-template-rows: repeat(auto-fill, 100px);
  gap: 15px;
  padding: 15px;
  flex-grow: 1;
  width: 100%;
}
.cell {
  border-color: v-bind(color);
  border-width: 1px;
  border-style: solid;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.cell:hover {
  border-color: green;
}
.cell.selected {
  background-color: green;
}
</style>
