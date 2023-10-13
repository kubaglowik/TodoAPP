<template>
  <option :value="modelValue">{{ text }}</option>
</template>
<script>
export default {
      name: 'AtomOption',
      props:{
      modelValue: {
      type: String,
      default: ''
      },
      text: {
      type: String,
      default: ''
      }
}
}
</script>
<style>
</style>