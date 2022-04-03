<template>
  <button class="button">
    {{title}}
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    title: {
      type: String
    }
  },
  data () {
    return {
    }
  }
}
</script>

<style scoped>
.button{
  background-color: #89A0B0;
  border-radius: 8px;
  color: white;
  cursor: pointer;
  padding: 8px 27px;
  border: none;
}
</style>
