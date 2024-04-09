<template>
  <div class="content">
    <span class="header">{{ item.name }}</span>

    <div class="detail" v-for="attr in innerItem.attributes" :key="attr.code">
      <div class="field">
        <span class="title">code:</span>
        <input :value="attr.code" />
      </div>

      <div class="field">
        <span class="title">name:</span>
        <input :value="attr.name" />
      </div>

      <template v-if="isColorAttribute(attr)">
        <div class="field">
          <span class="title">color:</span>
          <input :value="attr.color" />
        </div>
      </template>

      <template v-if="isSizeAttribute(attr)">
        <div class="field">
          <span class="title">size:</span>
          <span>
            <input :value="attr.size.width" type="number" /> x
            <input :value="attr.size.height" type="number" />
          </span>
        </div>
      </template>

      <template v-if="isWeightAttribute(attr)">
        <div class="field">
          <span class="title">weight:</span>
          <input :value="attr.weight" type="number" />
        </div>
      </template>
    </div>

    <div class="add">
      <label for="attributeType">type:</label>
      <select id="attributeType" v-model="selectedType">
        <option value="color">color</option>
        <option value="size">size</option>
        <option value="weight">weight</option>
      </select>

      <button @click="handleAddAttribute">Add</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, computed } from 'vue'
import { Color, Product, Size, Weight } from './types'

const props = defineProps<{
  item: Product
}>()

const innerItem = computed(() => props.item)
const emit = defineEmits(['click'])

const isColorAttribute = (attr: Color | Size | Weight): attr is Color =>
  'color' in attr

const isSizeAttribute = (attr: Color | Size | Weight): attr is Size =>
  'size' in attr

const isWeightAttribute = (attr: Color | Size | Weight): attr is Weight =>
  'weight' in attr

let selectedType: 'color' | 'size' | 'weight' = 'color'

const handleAddAttribute = () => {
  emit('click', selectedType)
}
</script>

<style scoped lang="css">
.header {
  font-weight: bold;
}
.content {
  display: flex;
  flex-direction: column;
  padding: 20px;
  gap: 20px;
}
.detail {
  padding: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.field {
  display: flex;
  gap: 5px;
}
.title {
  font-weight: bold;
}
.add {
  display: flex;
  gap: 10px;
}
</style>
