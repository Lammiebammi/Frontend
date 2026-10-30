<script setup>
    import axios from 'axios'

    const apiUrl = "api url goes here"
    var records = []

    try{
        const response = await axios.get(apiUrl)
        records = response.data
    }catch(ex){
        alert(ex.message)
    }
</script>

<template>
    <table>
        <thead>
            <tr>
                <th>Title</th>
                <th>Artist</th>
                <th>Duration</th>
                <th>Year of Publication</th>
                <th>Genre</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="record in records">
                <td>{{ record.title }}</td>
                <td>{{ record.artist }}</td>
                <td>{{ record.duration }}</td>
                <td>{{ record.publicationYear }}</td>
                <td>{{ record.genre }}</td>
            </tr>
        </tbody>
    </table>
</template>