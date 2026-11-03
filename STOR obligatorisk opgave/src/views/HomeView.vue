<script setup>
import { onMounted } from 'vue'
import TheWelcome from '../components/TheWelcome.vue'
import Axios from 'axios'

onMounted()

async function GetData() {
  const response = await Axios.get('https://localhost:7210/api/records', {
    headers: {
      'Content-Type': 'application/json; charset=utf-8',
    },
  })
  console.table(await response.data)
}

</script>

<template>
  <main></main>
  <button @click="GetData">get data</button>
</template>
