<template>
  <div class="main">
    <item-category :items="data" class="sidebar" @click="selectItem" />
    <item-content v-if="selectedItem" :item="selectedItem" />
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
