<template>
  <div class="main">
    <item-category :items="data" class="sidebar" @click="selectItem" />
    <item-content v-if="selectedItem" :item="selectedItem" @click="onClick" />
  </div>
</template>

<script setup lang="ts">
import { ref, Ref } from 'vue';

import ItemCategory from '@/components/ItemCategory.vue';
import ItemContent from '@/components/ItemContent.vue';

import Data from '@/common/mocks/mockData';
import { Product } from '@/types/types';

const data: Ref<Product[]> = ref(Data);
const selectedItem: Ref<Product | null> = ref(null);

const selectItem = (item: Product) => {
  selectedItem.value = item;
};

const onClick = (value: string) => {
  if (selectedItem.value) {
    switch (value) {
      case 'color': {
        selectedItem.value.attributes.push({
          code: 'new code',
          name: 'new field',
          color: 'color',
        });
        break;
      }
      case 'size': {
        selectedItem.value.attributes.push({
          code: 'new code',
          name: 'new field',
          size: {
            width: 0,
            height: 0,
          },
        });
        break;
      }
      case 'weight': {
        selectedItem.value.attributes.push({
          code: 'new code',
          name: 'new field',
          weight: 0,
        });
        break;
      }
    }
  }
};
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
