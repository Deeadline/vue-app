<template>
  <div class="wrapper">
    <Dogs v-model="dogLimit"
     @input="variables"/>

    <div class="imageResult" v-if="results !== null">
      <dog-image v-for="result in results" :key="result.id" :result="result" />
    </div>
  </div>
</template>

<script>
import Dogs from "@/components/Dogs.vue";
import DogImage from "@/components/DogsImage.vue";
import {debounce, axios, baseUrl, header} from "@/Constants.js";

export default {
  name: "App",
  components: {
    Dogs,
    DogImage,
  },
  data() {
    return {
      results: [],
      dogLimit: null,
    };
  },
  methods: {
    showPuppies: debounce(function() {
      axios
        .get(
          `${baseUrl}?size=med&mime_types=jpg&format=json&limit=${this.dogLimit}`,
          header
        )
        .then(response => {
          this.results = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    }, 400),
    errorLogs: () => {
      console.log(`${this.dogLimit} not found!`);
    },
  },
  computed: {
    variables: function(){
      (this.dogLimit !== null && this.dogLimit.indexOf(' ') < 0) ? showPuppies : errorLogs;
    },
  },
};
</script>


<style lang="scss" scoped>
body{
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  margin:0;
  padding: 0;
}
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  padding: 15px;
  margin: 0;
  min-height: 50vh;
  position: relative;
}
.imageResult {
  max-width: 70vw;
    margin-top: 50px;
    display: flex;
    flex-direction:row;
    flex-wrap: wrap;
  }
</style>
