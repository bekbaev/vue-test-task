<template>
  <div>
    <ItemsList :item="item" />
    <ItemAdd :item="item" />
  </div>
</template>

<script setup lang="ts">
import ItemsList from './ItemsList.vue';
import ItemAdd from './ItemAdd.vue';
import { Product } from '@/types/types';
import { defineProps } from 'vue';

defineProps<{
  item: Product;
}>();
</script>
