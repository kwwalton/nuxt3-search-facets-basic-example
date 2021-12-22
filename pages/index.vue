<template>
  <div class="search-page">
    <header>
      <h1>Search Results for Fruit</h1>
    </header>
    <aside>
      <FilterCheckboxes :title="title" :items="items" @change="handleChange" />
    </aside>
    <section>
      <Results :categories-to-show="checkedItems" />
    </section>
    <footer>
      <hr />
      <p>
        A basic example of how search facets work. 3 parts; checkboxes/facets,
        results list, and a controller/parent.
      </p>
    </footer>
  </div>
</template>

<script setup lang="ts">
// NOTE: Basic example of how search facets are implemented.
import { computed, reactive } from 'vue'
import { Iitem } from '~/types'

const title = 'fruit'
const items: Array<Iitem> = reactive([
  {
    label: 'Apple',
    value: 'apple',
    checked: true
  },
  {
    label: 'Banana',
    value: 'banana',
    checked: false
  },
  {
    label: 'Cherry',
    value: 'cherry',
    checked: false
  }
])
const checkedItems = computed(() =>
  items.filter((item) => item.checked).map((item) => item.value)
)
const handleChange = (event: { checked: boolean; value: string }) => {
  const index = items.findIndex((item) => item.value === event.value)
  if (index !== -1) {
    items[index].checked = event.checked
  }
  // NOTE: this would be part of payload to search call
  console.log('checkedItems', checkedItems.value)
}
</script>

<style scoped></style>
