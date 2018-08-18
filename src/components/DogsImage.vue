<template>
<div :style="style" class="imageWrapper"/>
</template>

<script>
export default {
  name: "DogImage",
  props: {
    result: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      imageUrl: this.result.url,
    };
  },
  computed: {
      style() {
          return `background-image: url("${this.imageUrl}")`;
      }
  }
};
</script>


<style lang="scss" scoped>
.imageWrapper {
  width: 30vh;
  height: 200px;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 50%;
  margin-top: 5px;
  margin-right: 5vh;
}
</style>
