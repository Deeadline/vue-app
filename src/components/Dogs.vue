<template>
<div class="DogWrapper">
    <p>How many dogs do you want to see?</p>
    <input @input="sendProperty"
     :value="value"
      :placeholder="value || placeholder"/>
</div>
</template>

<script>
export default {
    name: 'Hello',
    props: {
        value: {
            required: true,
        },
    },
    data() {
        return {
            placeholder:  '',
        }
    },
    methods: {
        sendProperty(e) {
            this.$emit('input', e.target.value);
        }
    },
}
</script>

<style lang="scss" scoped>
.DogWrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  p {
    font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS",
      sans-serif;
    padding-bottom: 15px;
  }
  input {
    height: 25px;
    border: 0;
    border-bottom: 1px solid black;
    text-align: center;
  }
}
</style>
