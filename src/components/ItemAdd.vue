<template>
  <div class="add">
    <label
      >Type
      <select v-model="selectedType">
        <option value="color">Color</option>
        <option value="size">Size</option>
        <option value="weight">Weight</option>
      </select>
    </label>

    <form class="form" @submit.prevent="addItem">
      <label v-for="(field, label) in formFields[selectedType]" :key="label"
        >{{ label }}
        <input
          v-model="formData[label]"
          :type="field.type"
          :placeholder="field.placeholder" />
      </label>
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script setup lang="ts">
import { Color, Product, Size, Weight } from '@/types/types';
import { computed, defineProps, ref } from 'vue';

const props = defineProps<{
  item: Product;
}>();

const innerItem = ref(props.item);

const formFields = ref({
  color: {
    Code: { type: 'text', value: '', placeholder: 'please enter code' },
    Name: { type: 'text', value: '', placeholder: 'please enter name' },
    Color: { type: 'text', value: '', placeholder: 'please enter color' },
  },
  size: {
    Code: { type: 'text', value: '', placeholder: 'please enter code' },
    Name: { type: 'text', value: '', placeholder: 'please enter name' },
    Width: { type: 'number', value: 0 },
    Height: { type: 'number', value: 0 },
  },
  weight: {
    Code: { type: 'text', value: '', placeholder: 'please enter code' },
    Name: { type: 'text', value: '', placeholder: 'please enter name' },
    Weight: { type: 'number', value: 0 },
  },
});

let selectedType = ref<'color' | 'size' | 'weight'>('color');
let formData = computed(() =>
  Object.fromEntries(
    Object.entries(formFields.value[selectedType.value]).map(([label, field]) => [
      label,
      field.value,
    ]),
  ),
);

const addItem = () => {
  let newAttribute: Color | Size | Weight;

  switch (selectedType.value) {
    case 'color':
      newAttribute = {
        code: formData.value.Code as string,
        name: formData.value.Name as string,
        color: formData.value.Color as string,
      };
      break;
    case 'size':
      newAttribute = {
        code: formData.value.Code as string,
        name: formData.value.Name as string,
        size: {
          width: formData.value.Width as number,
          height: formData.value.Height as number,
        },
      };
      break;
    case 'weight':
      newAttribute = {
        code: formData.value.Code as string,
        name: formData.value.Name as string,
        weight: formData.value.Weight as number,
      };
      break;
    default:
      throw new Error('Invalid attribute type');
  }

  innerItem.value.attributes.push(newAttribute);
};
</script>

<style scoped>
.add {
  max-width: 300px;
}

.form {
  margin-top: 20px;
}

.form label {
  display: block;
  margin-bottom: 10px;
}

.form input {
  width: 100%;
  padding: 5px;
  margin-top: 5px;
}

.form button {
  margin-top: 10px;
}
</style>
