<template>
  <div class="wrapper">
    <Dogs></Dogs>
  </div>
</template>

<script>
import Dogs from '@/components/Dogs.vue';
export default {
  name: 'App',
  components: {
    Dogs,
  },
}
</script>


<style lang="scss" scoped>
.wrapper {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  display: flex;
  flex-direction: column;
  height: 100vh;
  padding: 0;
  margin: 0;
}
</style>
