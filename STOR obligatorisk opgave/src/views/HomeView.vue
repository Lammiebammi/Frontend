<script setup>
import { onMounted, ref } from 'vue'
import Axios from 'axios'

const array = ref(null)
const titleInput = ref(null)
const artistInput = ref(null)
const durationInput = ref(null)
const yearInput = ref(null)
const genreInput = ref(null)

onMounted(async () => {
  await SearchData()
})

function CleanUp() {
  titleInput.value = null
  artistInput.value = null
  durationInput.value = null
  yearInput.value = null
  genreInput.value = null
}

async function SearchData() {
  console.log(titleInput.value)
  const searchAPI = ref('https://localhost:7210/api/records?')
  if (titleInput.value != null)
    searchAPI.value = searchAPI.value.concat('title=' + titleInput.value, '&')
  if (artistInput.value != null)
    searchAPI.value = searchAPI.value.concat('artist=' + artistInput.value, '&')
  if (durationInput.value != null)
    searchAPI.value = searchAPI.value.concat('duration=' + durationInput.value, '&')
  if (yearInput.value != null)
    searchAPI.value = searchAPI.value.concat('publicationYear=' + yearInput.value, '&')
  if (genreInput.value != null)
    searchAPI.value = searchAPI.value.concat('genre=' + genreInput.value, '&')
  searchAPI.value = searchAPI.value.slice(0, -1)
  const response = await Axios.get(searchAPI.value)
  console.log(searchAPI.value)
  array.value = response.data
  //console.table(response.data)
  //CleanUp()
}
</script>

<template>
  <main>
    <div>
      <input type="text" placeholder="Title..." v-model="titleInput" />
      <input type="text" placeholder="Artist..." v-model="artistInput" />
      <input type="text" placeholder="Duration in seconds..." v-model="durationInput" />
      <input type="text" placeholder="Year..." v-model="yearInput" />
      <input type="text" placeholder="Genre..." v-model="genreInput" />
      <button @click="SearchData">Search</button>
    </div>
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
  </main>
</template>
