<template>
<div class="DogWrapper">
    <label for="dogInput">How many dogs do you want to see?</label>
    <input v-model="dogLimit" :placeholder="placeholder">
    <button @click="showPuppies(dogLimit)">Submit</button>

    <div v-for="result in results" :key="result.id">
        <img :src="result.url" />
    </div>
</div>
</template>

<script>
const axios = require('axios');
const baseUrl = "https://api.thedogapi.com/v1/images/search";
const header = {
    headers: {'x-api-key': 'a8589ed6-0d78-4ee2-b333-a2caf465c342'}
};
export default {
    name: 'Hello',
    data() {
        return {
            results: [],
            dogLimit: null,
            placeholder: "From 1 to 25",
        };
    },
    methods: {
        showPuppies(dogLimit) {
            axios.get(`${baseUrl}?size=med&mime_types=jpg&format=json&limit=${dogLimit}`, header).then( (response) => {
                this.results = response.data;
            })
            .catch((error)=> {
                console.log(error)
            });
        }
    }
}
</script>

<style lang="scss" scoped>
.DogWrapper{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
label{
    padding-bottom: 5px;
}
</style>
