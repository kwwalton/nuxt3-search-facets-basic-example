<template>
  <form class="filter-checkboxes" @submit="handleSubmit">
    <h3 class="filter-checkboxes__title">
      {{ title }}
    </h3>
    <ul class="filter-checkboxes__list">
      <li
        class="filter-checkboxes__list-item"
        v-for="(item, index) in items"
        :key="index"
      >
        <label class="filter-checkboxes__list-item-label">
          <input
            type="checkbox"
            v-model="item.checked"
            v-bind:value="item.value"
            @change="handleChange($event)"
          />
          <span>{{ item.label }}</span>
        </label>
      </li>
    </ul>
  </form>
</template>

<script setup lang="ts">
import { Iitem } from '~/types'

const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  items: {
    type: Array,
    default: [] as Array<Iitem>
  }
})

const emit = defineEmits(['change'])

const handleChange = (event: Event) => {
  const checked = (event.target as HTMLInputElement).checked
  const value = (event.target as HTMLInputElement).value
  emit('change', { checked, value })
}
</script>

<style scoped>
ul.filter-checkboxes__list {
  list-style: none;
  padding: 0;
}
</style>
