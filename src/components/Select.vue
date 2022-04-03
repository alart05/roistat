<template>
  <select class="select">
    <option></option>
    <option v-for="(option, index) in options" :key="index">
      {{ option.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'Select',
  props: {
    options: {type: Array, default: () => []}
  }
}
</script>

<style scoped>
.select{
  width: 100%;
  box-sizing: border-box;
  border: 1px solid #89A0B0;
  border-radius: 4px;
  background-color: transparent;
}
.select:active, .select:hover, .select:focus {
  outline: 0;
  outline-offset: 0;
}
</style>
