<template>
  <button class="btn-blue">{{ buttonText }}</button>
</template>

<script>
export default {
  name: 'b-button',
  props: {
    buttonText: String
  }
}
</script>

<style scoped>
.btn-blue {
  color: blue;
  border: 1px solid blue;
  background: transparent;
  padding: 10px;
  font-size: 1em;
  min-width: 100px;
  cursor: pointer;
}
</style>