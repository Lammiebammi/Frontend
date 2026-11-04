<script setup>
import { onMounted, ref } from 'vue'
import Axios from 'axios'

const array = ref(null)

onMounted(async () => {
  await GetData()
})

async function GetData() {
  const response = await Axios.get('https://localhost:7210/api/records')
  array.value = response.data
  console.table(response.data)
  //array = await response.data
}
</script>

<template>
  <main></main>
  <table>
    <thead>
      <tr>
        <th>id</th>
        <th>title</th>
        <th>artist</th>
        <th>duration</th>
        <th>year</th>
        <th>genre</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="a in array">
        <td>{{ a.id }}</td>
        <td>{{ a.title }}</td>
        <td>{{ a.artist }}</td>
        <td>{{ a.duration }}</td>
        <td>{{ a.publicationYear }}</td>
        <td>{{ a.genre }}</td>
      </tr>
    </tbody>
  </table>
</template>
