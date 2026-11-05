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
  //console.log(titleInput.value)
  const searchAPI = ref('https://soo-backend-g8ffhpadhhc7etbn.swedencentral-01.azurewebsites.net/api/records?')
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
  //console.log(searchAPI.value)
  array.value = response.data
  //console.table(response.data)
  CleanUp()
}

function UniqueElementId(param1, param2) {
  const newTitle = param2.replace(' ', '-')
  return `${param1}-${newTitle.toLowerCase()}`
}
</script>

<template>
  <main>
    <div>
      <input type="text" placeholder="Title..." v-model="titleInput" id="title-search-bar" />
      <input type="text" placeholder="Artist..." v-model="artistInput" id="artist-search-bar" />
      <input
        type="number"
        placeholder="Duration in seconds..."
        v-model="durationInput"
        id="duration-search-bar"
      />
      <input type="text" placeholder="Year..." v-model="yearInput" id="year-search-bar" />
      <input type="text" placeholder="Genre..." v-model="genreInput" id="genre-search-bar" />
      <button @click="SearchData" id="search-button">Search</button>
    </div>
    <table>
      <thead>
        <tr class="tr-th">
          <th>id</th>
          <th>title</th>
          <th>artist</th>
          <th>duration</th>
          <th>year</th>
          <th>genre</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="a in array" key="a.id" :id="UniqueElementId(a.id, a.title)" class="table-row">
          <td class="id">{{ a.id }}</td>
          <td class="title">{{ a.title }}</td>
          <td class="artist">{{ a.artist }}</td>
          <td class="duration">{{ a.duration }}</td>
          <td class="publicationyear">{{ a.publicationYear }}</td>
          <td class="genre">{{ a.genre }}</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
