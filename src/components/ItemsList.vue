<template>
  <div class="content">
    <span class="header">{{ innerItem.name }}</span>

    <div class="detail" v-for="attr in innerItem.attributes" :key="attr.code">
      <div class="field">
        <span class="title">code:</span>
        <input :value="attr.code" />
      </div>

      <div class="field">
        <span class="title">name:</span>
        <input :value="attr.name" />
      </div>

      <div v-if="'color' in attr" class="field">
        <span class="title">color:</span>
        <input :value="attr.color" />
      </div>

      <div v-if="'size' in attr" class="field">
        <span class="title">size:</span>
        <span>
          <input :value="attr.size.width" type="number" /> x
          <input :value="attr.size.height" type="number" />
        </span>
      </div>

      <div v-if="'weight' in attr" class="field">
        <span class="title">weight:</span>
        <input :value="attr.weight" type="number" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Product } from '@/types/types';
import { defineProps, ref, watch } from 'vue';

const props = defineProps<{
  item: Product;
}>();

const innerItem = ref(props.item);

watch(
  () => props.item,
  () => {
    innerItem.value = props.item;
  },
);
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
</style>
