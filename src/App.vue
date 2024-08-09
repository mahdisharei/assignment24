<script setup>
import {ref, computed} from 'vue';

const search = ref('')
const users = ref([])
const results = computed(() => {
  if (search.value.length > 0) {
    return users.value.filter((item) => item.name.toLowerCase().includes(search.value.toLowerCase()))
  }
})

const useFetch = async (url) => {
  const response = await fetch(url)
  return await response.json()
}

const getUsers = async () => {
  const data = await useFetch('https://jsonplaceholder.typicode.com/users')
  users.value = data
}
</script>

<template>
  <button @click="getUsers">get the list</button>
  <ul>
    <li v-for="user in users">
      {{ user.name }}
    </li>
  </ul>
  <input v-model="search" type="text" placeholder="search">
  <ul>
    <li v-for="result in results">
      {{ result.name }}
    </li>
  </ul>
</template>

<style>
input {
  display: block;
  margin-top: 5px;
}
</style>


