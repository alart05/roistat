<template>
  <input
    v-model="text"
    :type="type"
    class="input"
    :class="haveError ? 'error' : ''
  ">
</template>

<script>
export default {
  name: 'Input',
  props: {
    haveError: { type: Boolean, default: false },
    type: { type: String, default: 'text' }
  },
  data () {
    return {
      text: ''
    }
  },
  watch: {
    text () {
      this.$emit('update', this.text)
    }
  }
}
</script>

<style scoped>
.input{
  width: 100%;
  box-sizing: border-box;
  border: 1px solid #89A0B0;
  border-radius: 4px;
  background-color: transparent;
}
.input:active, .input:hover, .input:focus {
  outline: 0;
  outline-offset: 0;
}
.error {
  border-color: red;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
input[type='number'],
input[type="number"]:hover,
input[type="number"]:focus {
  appearance: none;
  -moz-appearance: textfield;
}
</style>
