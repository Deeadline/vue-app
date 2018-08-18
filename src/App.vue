<template>
  <div class="wrapper">
    <Dogs v-model="dogLimit"
     @input="runProperlyFunction"/>

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
      dogLimit: '',
    };
  },
  methods: {
    runProperlyFunction: function(){
      if(this.dogLimit !== '' && this.dogLimit.indexOf(' ') < 0) {
        return { input: this.showPuppies() };
      }
      return { input : this.errorLogs() };
    },
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
    errorLogs: function () {
      alert(`Dog limit not found!`);
      location.reload();
    },
  },
};
</script>


<style lang="scss" scoped>
body{
  font-family:Arial, Helvetica, sans-serif;
  font-size: 16px;
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
