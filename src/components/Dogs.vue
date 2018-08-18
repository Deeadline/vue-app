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
            type: String,
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
            if(e.target.value.indexOf(' ') < 0)
                this.$emit('input', e.target.value);
            else
                this.$emit('input', '');
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
