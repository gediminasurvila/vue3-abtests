<template>
  <button class="btn-red gtm-abtest">{{ buttonText }}</button>
</template>

<script>
export default {
  name: 'a-button',
  props: {
    buttonText: String
  }
}
</script>

<style scoped>
.btn-red {
  color: red;
  border: 1px solid red;
  background: transparent;
  padding: 10px;
  font-size: 1em;
  min-width: 100px;
  cursor: pointer;
}
</style>