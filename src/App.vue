<template>
  <div class="main">
    <item-list :items="data" class="sidebar" @click="handleSelectItem" />
    <item-content
      v-if="selectedItem"
      :item="selectedItem"
      @click="handleAddContent"
    />
  </div>
</template>

<script setup lang="ts">
import ItemList from './components/ItemList.vue'
import ItemContent from './components/ItemContent.vue'
import Data from './components/mockData'
import { ref } from 'vue'
import { Product } from './components/types'

const data = ref(Data)

const selectedItem = ref()

const handleSelectItem = (item: Product) => {
  selectedItem.value = item
}

const handleAddContent = (value: any) => {
  switch (value) {
    case 'color': {
      selectedItem.value?.attributes.push({
        code: 'new code',
        name: 'new field',
        color: 'color',
      })
      break
    }
    case 'size': {
      selectedItem.value?.attributes.push({
        code: 'new code',
        name: 'new field',
        size: {
          width: 0,
          height: 0,
        },
      })
      break
    }
    case 'weight': {
      selectedItem.value?.attributes.push({
        code: 'new code',
        name: 'new field',
        weight: 0,
      })
      break
    }
  }
}
</script>

<style scoped lang="css">
.main {
  display: flex;
  gap: 20px;
}
.sidebar {
  width: auto;
}
</style>
