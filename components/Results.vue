<template>
  <ul class="results">
    <li v-for="item in filteredItems" :key="item.id">
      <a :href="item.url">
        <h3>{{ item.title }}</h3>
        <p>{{ item.description }}</p>
      </a>
    </li>
  </ul>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  categoriesToShow: {
    type: Array,
    default: [] as Array<string>
  }
})
// NOTE: items does not need to be reactive, its acting like a json object from the server.
// You would do all this filtering in your api and we would just present the results.
const items = [
  { title: 'Apple', description: 'apple', category: 'apple', url: '#' },
  { title: 'Apple', description: 'apple', category: 'apple', url: '#' },
  { title: 'Apple', description: 'apple', category: 'apple', url: '#' },
  { title: 'Apple', description: 'apple', category: 'apple', url: '#' },
  { title: 'Banana', description: 'banana', category: 'banana', url: '#' },
  { title: 'Banana', description: 'banana', category: 'banana', url: '#' },
  { title: 'Cherry', description: 'cherry', category: 'cherry', url: '#' }
]
const filteredItems = computed(() =>
  items.filter((item) => props.categoriesToShow.includes(item.category))
)
</script>

<style scoped>
ul.results {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}
ul.results li {
  padding: 1rem;
  border: 1px solid #ccc;
}
ul.results li:hover {
  background: #eee;
}
@media screen and (max-width: 600px) {
  ul.results {
    grid-template-columns: 1fr;
  }
}
</style>
